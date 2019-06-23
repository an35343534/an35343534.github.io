---
layout: post
title: 《笨方法学写作》电子书免费下载
date: 2019-12-31
categories: blog
tags: [读书,卡片]
description: 读书是一项「对重要内容进行提炼的工序」。
---

## Links

https://stuartsierra.com/2018/07/06/threading-with-style

## Text

threads like

```clojure
(-> input
    step-one
    step-two
    step-three
    result)
```

for navigation

```clojure
;; 1
(-> results :matches (nth 3) :scores (get "total_points"))

;; 2
(-> results .getMatches (nth 3) .getScores (.getKey "total_points))
```



type hints for eliminate reflections

```clo
(let [m {:now (Date.)}]
  ;; We can't type-hint a keyword, so wrap it in a list:
  (-> m ^Date (:now) .getTime))
```

```clojure
(.. results getMatches (getItem 3) getScores (getKey "total_points))
```

Transformations

```clojure
(-> geme-state
    (assoc :next-player :player2)
    (update :turn-counter inc)
    (update-in [:scores :player1] + 10)
    (update-in [:scores :player2] - 3))
```

sequences

```clojure
(->> data
     (map :players)
     (mapcat :scores)
     (filter #(< 100 %))
     sort)
```

Dont's

```clojure
;; BAD
(-> data
    :matches
    (->> (map :final-score)
         (reduce +)))
;; BAD
(-> celsius
    (* 9)
    (/ 5)
    (+ 32))
;; BAD
(-> results
    :matches
    (#(filter winning-match? %))
    (nth 3)
    :scores
    (get "total_points"))
;; BAD
(->> rdr 
     line-seq
     (map parse-line)
     set
     (with-open [rdr (io/reader file)])
     (def lines))
```

```clojure
;; Assuming require [clojure.tools.logging :as log]
(Thread/setDefaultUncaughtExceptionHandler
 (reify Thread$UncaughtExceptionHandler
   (uncaughtException [_ thread ex]
     (log/error ex "Uncaught exception on" (.getName thread)))))

(defn process-batch [items]
  {:pre [(coll? items)]}
  ;; ... 
  )
```

