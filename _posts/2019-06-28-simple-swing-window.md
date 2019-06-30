---
layout: post
title: swing jvm
date: 2019-06-27
categories: blog
tags: swing, java, clojure
description: todo
---

# WIP

## java

...

## clojure

```clojure
(ns cljpil.core
  (:gen-class)
  (:require
    [cljpil.obj-parser :as obj])
  (:require
    [taoensso.timbre :as timbre
     :refer [log  trace  debug  info  warn  error  fatal  report
             logf tracef debugf infof warnf errorf fatalf reportf
             spy get-env]])
  (:require [taoensso.timbre.appenders.core :as appenders])
  (:import
    (javax.swing JFrame JComponent JButton)
    (java.awt Dimension GridBagLayout GridBagConstraints Color EventQueue Graphics)
    (java.awt.image BufferedImage)
    (java.awt.event ActionListener)
    (SwingZ.JRasterizer Lesson3 Lesson2 Lesson1 Lesson0 L3 L2 L1 L0)))

;;; Logging ;;;;;;;;;;;;;;;;;;;;

(timbre/merge-config!
  {:appenders {:spit (appenders/spit-appender {:fname "my-file.log"})}})

;; (timbre/merge-config! {:appenders {:spit {:enabled? false}}} ; To disable
;; (timbre/merge-config! {:appenders {:spit nil}}               ; To remove entirely

(info "Program started")


;;; Program ;;;;;;;;;;;;;;;;;;;;

(def xsize 800)

(defn toInt [x]
  (if (>= x (bit-shift-left 1 31))
    (bit-shift-right (bit-shift-left x 32) 32)
    x))

(def colors {:red (toInt 0xffff0000)
             :blue (toInt 0xff0000ff)
             :green (toInt 0xff00ff00)
             :black (toInt 0xff000000)
             :white (toInt 0xffffffff)})


(def vs obj/vs)
(def fs obj/fs)


(def angle (atom 0.0))

;; Angle in degrees
(def angleLR (atom 30))
(def angleUD (atom 0))






(def component
  (proxy [JComponent] []
    (getPreferredSize []
      (Dimension. xsize xsize))))



#_(defn swingz []
    (let [img (Lesson0. xsize)]
      (.run img)
      (.save img "savefromclj")
      (.getBufferedImage img)))

(defn normalize [[[f1 g1 h1] [f2 g2 h2] [f3 g3 h3]]]
  (let [vx1 (- f1 f2)
        vy1 (- g1 g2)
        vz1 (- h1 h2)
        vx2 (- f2 f3)
        vy2 (- g2 g3)
        vz2 (- h2 h3)]

    [(- (* vy1 vz2) (* vy2 vz1))
     (- (* vx1 vz2) (* vx2 vz1))
     (- (* vy1 vx2) (* vy2 vx1))]))

(defn swingz []
  (let [pi (L2. xsize)]
    ;(.test pi)

    (doseq [t (->> fs
                   (map (fn [[a b c]] [(get vs (dec a)) (get vs (dec b)) (get vs (dec c))]))

                   (map #(map (fn [[x y z]] [(+
                                               (* x
                                                  (Math/cos (* @angleLR 1/180 Math/PI)))
                                               (* z
                                                  (Math/sin (* @angleLR 1/180 Math/PI))))
                                             y
                                             (- (* z -2) 3)
                                             #_(+ -2
                                                 (* x
                                                    (Math/sin (* @angleLR 1/180 Math/PI)))
                                                 (* z
                                                    -1
                                                    (Math/cos (* @angleLR 1/180 Math/PI ))))]) %))
                   (map (fn [[p1 p2 p3]]
                          [(map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p1)
                           (map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p2)
                           (map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p3)]))
                   (map #(map int-array %)))]
      (.drawTriangle pi (first t) (second t) (last t) ((fn [x] (toInt (+ 0xff000000  (* (int x) 256) ))) (+ 150 (apply + (map * (normalize t) [0 0 -0.04])))))
      (println (apply + (map * (normalize t) [0 0 1]))))



    (.getBufferedImage pi)))




#_(defn proto-ints []
    (let [data (int-array (* xsize xsize) (toInt 0xff000000))
          color (toInt 0xffff00ff)
          zbuffer (int-array (* xsize xsize) 255)]
        ;(horizontal-line data 20 100 80 color)
        ;(set-pixel data 200 80 color)
        ;(do
        ;  (line data 100 100 190 100 color)
        ;  (line data 100 100 190 190 color)
        ;  (line data 100 100 190 10 color)
        ;  (line data 100 100 100 190 color)
        ;  (line data 100 100 100 10 color)
        ;
        ;  (line data 100,100, 10,10 color)
        ;  (line data 100,100, 10,100 color)
        ;  (line data 100,100, 10,190 color))

        #_(dorun
            (pmap
              #(let [[a b c] %]
                 (line data (first a) (second a) (first b) (second b) color)
                 (line data (first a) (second a) (first c) (second c) color)
                 (line data (first c) (second c) (first b) (second b) color))
              (->> fs
                   (map (fn [[a b c]] [(get vs (dec a)) (get vs (dec b)) (get vs (dec c))]))

                   (map #(map (fn [[x y z]] [(+
                                               (* x
                                                  (Math/cos (* @angleLR 1/180 Math/PI)))
                                               (* z
                                                  (Math/sin (* @angleLR 1/180 Math/PI )))) y]) %))
                   (map (fn [[p1 p2 p3]]
                          [(map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p1)
                           (map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p2)
                           (map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p3)]))
                   (map #(map int-array %)))))

        ;(fill-triangle data [10 10]  [380 180] [150 390] color)
        (dorun
          (map
            (fn [[a b c]]
              (line data zbuffer a b color)
              (line data zbuffer a c color)
              (line data zbuffer c b color)
              (fill-triangle data zbuffer a b c color))
            (->> fs
                 (map (fn [[a b c]] [(get vs (dec a)) (get vs (dec b)) (get vs (dec c))]))

                 (map #(map (fn [[x y z]] [(+
                                             (* x
                                                (Math/cos (* @angleLR 1/180 Math/PI)))
                                             (* z
                                                (Math/sin (* @angleLR 1/180 Math/PI )))) y z]) %))
                 (map (fn [[p1 p2 p3]]
                        [(map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p1)
                         (map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p2)
                         (map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p3)])))))
        data))
     ; zbuffer))

;(defn im []
;  (let [image (BufferedImage. xsize xsize BufferedImage/TYPE_INT_ARGB)]
;    (.setRGB image 0 0 xsize xsize (proto-ints) 0 xsize)
;    image))




(def button1 (JButton. "<--"))
(def button2 (JButton. "-->"))

(def button-repaint (JButton. "repaint"))

(.addActionListener button1 (reify ActionListener
                              (actionPerformed [_ e]
                                (do
                                  (swap! angleLR #(mod (- % 3) 360))
                                  (.repaint component)))))

(.addActionListener button2 (reify ActionListener
                              (actionPerformed [_ e]
                                (do
                                  (swap! angleLR #(mod (+ % 3) 360))
                                  (.repaint component)))))

(def component (proxy [JComponent] []
                 (getPreferredSize []
                   (Dimension. xsize xsize))
                 (paintComponent [^Graphics graphics]
                   (.drawImage graphics (swingz) 0 0 nil)
                   nil)))

(defn window []
  (doto (JFrame.)
    (.setTitle "window1")
    (.setLayout (GridBagLayout.))
    (.add button1 (GridBagConstraints.))
    (.add button2 (let [constr (GridBagConstraints.)]
                    (set! (.gridx constr) 1)
                    constr))
    (.add component (let [constr (GridBagConstraints.)]
                      (set! (.gridy constr) 1)
                      (set! (.-gridwidth constr) 3)
                      constr))
    (.pack)
    (.setVisible true)))



(defn run []
  (doto ^JFrame (window)
      (.setDefaultCloseOperation JFrame/EXIT_ON_CLOSE)
      (.setVisible true)))

(defn -main []
  (println "hi")
  (EventQueue/invokeLater window))


;;;

(apply max (->> fs
                (map (fn [[a b c]] [(get vs (dec a)) (get vs (dec b)) (get vs (dec c))]))

                (map #(map (fn [[x y z]] [(+
                                            (* x
                                               (Math/cos (* @angleLR 1/180 Math/PI)))
                                            (* z
                                               (Math/sin (* @angleLR 1/180 Math/PI))))
                                          y
                                          z
                                          #_(+
                                              (* x
                                                 (Math/sin (* @angleLR 1/180 Math/PI)))
                                              (* z
                                                 (Math/cos (* @angleLR 1/180 Math/PI ))))]) %))
                (map (fn [[p1 p2 p3]]
                       [(map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p1)
                        (map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p2)
                        (map #(int (+ (* % 0.44 xsize) (/ xsize 2))) p3)]))
                (map #(map int-array %))
                (map #(+ 150 (apply + (map * (normalize %) [0 0 -0.04]))))))

```

