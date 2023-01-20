---
layout:   post
title:    "variadic functions"
date:     2023-01-20 12:46:00 +0700
category: clojure
tags:     clojure keyword-argument variadic function
---

```clj
; The beginning of the variable parameters is marked with &
(defn test [& opts]
  (prn opts))

(test "hello" "world")
;=> ("hello" "world")


; from clojure 1.11 it supports keyword arguments
(defn test2 [& {:keys [a b] :as opts}]
  (prn a b opts))

(test2 :a 1)
;=> 1 nil {:a 1}

(test2 {:a 1 :b 2})
;=> 1 2 {:a 1, :b 2}
```