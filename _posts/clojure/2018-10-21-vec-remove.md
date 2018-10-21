---
layout:   post
title:    "remove item from vector"
date:     2018-10-21 10:46:00 +0700
category: clojure
tags:     clojure vector
---

To remove the element at index `n` from vector `v`:
```clj
(defn remove-indexed [v n]
  (into (subvec v 0 n) (subvec v (inc n))))
```
