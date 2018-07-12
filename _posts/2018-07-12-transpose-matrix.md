---
layout: post
title:  "transpose matrix"
date:   2018-07-09 18:23:00 +0700
tags:   clojure transpose matrix
---

```clj
(defn transpose [col]
  (apply map vector col))

(def a [[5 4]
        [4 0]
        [7 10]
        [-1 8]])

(transpose a)
;=> ([5 4 7 -1]
;    [4 0 10 8])
```
