---
layout: post
title:  "apply fn to all value of a map"
date:   2018-06-22 14:30:00 +0700
tags:   clojure specter
---

```clj
(into {} (for [[k v] m]
           [k (f v)]))

; using Specter
(transform [MAP-VALS] inc {:a 1 :b 2 :c 3})
;=> {:a 2, :b 3, :c 4}
```
