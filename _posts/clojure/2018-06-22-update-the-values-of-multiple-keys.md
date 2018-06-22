---
layout: post
title:  "Update the values of multiple keys"
date:   2018-06-22 14:36:00 +0700
categories: [ clojure, map ]
---

```clj
(defn update-vals [m ks & args]
  (reduce #(apply update % %2 args) m ks))

(update-vals {:a 0 :b 1 :c 2} [:a :b] inc)
;;=> {:a 1, :b 2, c 2} 

(update-vals {:a 0 :b 1 :c 2} [:a :b] + 10)
;;=> {:a 10, :b 11, c 2}


;; using Specter
(transform (multi-path :a :b) inc {:a 0, :b 1, :c 2})
;=> {:a 1, :b 2, :c 2}

(transform [(submap [:a :b]) MAP-VALS] inc {:a 0, :b 1, :c 2})
;=> {:c 2, :a 1, :b 2}
```
