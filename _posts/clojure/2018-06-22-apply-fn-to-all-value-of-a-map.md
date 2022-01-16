---
layout: post
title:  "apply fn to all value of a map"
date:   2018-06-22 14:30:00 +0700
category: clojure
tags:   clojure specter map
---

*note: Clojure 1.11 now has new function: `(update-vals m f)` and `(update-keys m f)`.

https://clojure.github.io/clojure/branch-master/clojure.core-api.html#clojure.core/update-vals

```clj
(into {} (for [[k v] m]
           [k (f v)]))

; using Specter
(transform [MAP-VALS] inc {:a 1 :b 2 :c 3})
;=> {:a 2, :b 3, :c 4}
```
