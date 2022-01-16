---
layout:   post
title:    "ex-info & ex-data"
date:     2020-10-15 16:46:00 +0700
category: clojure
tags:     clojure exception error
---

```clj
; ex-info creates an instance of ExceptionInfo, a RuntimeException subclass
; that carries a map of additional data.
(defn div [x]
  (try
    (/ 3 x)
    (catch Exception e
      (throw (ex-info (.getMessage e) {:x x})))))

; ex-data returns exception map data from ExceptionInfo instance
(try
  (div 0)
  (catch Exception e
    (prn (.getMessage e)) ; "Divide by zero"
    (prn (ex-data e))     ; {:x 0}
    ))
```
