---
layout: post
title: simple networking
date: 2019-06-27
categories: blog
tags: java, clojure
description: todo
---

# WIP

## here will be article about networking

```clojure
(ns xtest.server
    (:gen-class)
    (:require [clojure.java.io :as io])
    (:import [java.net InetAddress ServerSocket Socket SocketException]))


(defn -main
  "I don't do a whole lot ... yet."
  [& args]
  
  (println "Hello, World!")
  (prn (+ 3 6)))




(defn- server-socket [server]
  (ServerSocket.
   (:port server)
   (:backlog server)
   (InetAddress/getByName (:host server))))

(defn handler [reader writer]
  (.append writer "Hello World\n"))

(defn tcp-server
  "Create a new TCP server. Takes the following keyword arguments:
    :host    - the host to bind to (defaults to 127.0.0.1)
    :port    - the port to bind to
    :handler - a function to handle incoming connections, expects a socket as
               an argument
    :backlog - the maximum backlog of connections to keep (defaults to 50)"
  [& {:as options}]
  #_{:pre [(:port options)
           (:handler handler)]}
  (merge
   {:host "127.0.0.1"
    :backlog 50
    :socket (atom nil)
    :connections (atom #{})}
   options))

(defn close-socket [server socket]
  (swap! (:connections server) disj socket)
  (when-not (.isClosed socket)
    (.close socket)))

(defn- open-server-socket [server]
  (reset! (:socket server)
          (server-socket server)))

(defn- accept-connection
  [{:keys [handler connections socket] :as server}]
  (let [conn (.accept @socket)]
    (swap! connections conj conn)
    (future
      (try (handler conn)
           (finally (close-socket server conn))))))

(defn running?
  "True if the server is running."
  [server]
  (if-let [socket @(:socket server)]
    (not (.isClosed socket))))

(defn start
  "Start a TCP server going."
  [server]
  (open-server-socket server)
  (future
    (while (running? server)
      (try
        (accept-connection server)
        (catch SocketException _)))))

(defn stop
  "Stop the TCP server and close all open connections."
  [server]
  (doseq [socket @(:connections server)]
    (close-socket server socket))
  (.close @(:socket server)))

(defn wrap-streams
  "Wrap a handler so that it expects an InputStream and an OutputStream
  as arguments, rather than a raw Socket."
  [handler]
  (fn [socket]
    (with-open [input  (.getInputStream socket)
                output (.getOutputStream socket)]
      (handler input output))))

(defn wrap-io
  "Wrap a handler so that it expects a Reader and Writer as arguments, rather
  than a raw Socket."
  [handler]
  (wrap-streams
   (fn [input output]
     (with-open [reader (io/reader input)
                 writer (io/writer output)]
       (handler reader writer)))))




(def server
  (tcp-server 
    :port    5000
    :handler (wrap-io handler)))

(start server)







(defn fun
    ([] (print "fun1!!\n"))
    ([x] (print (str x))))


(defn loader [f] f)

(defn fun [] (print "fun2!!\n"))




```