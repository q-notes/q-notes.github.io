---
layout: post
title:  "reload a multimethod in Clojure"
date:   2018-06-28 23:30:00 +0700
tags:   clojure multimethod
---

```clj
(defmulti greeting :language)
(defmethod greeting "English" [_] "Hello!")

(greeting {:language "English"})
;=> Hello!


;; At this point, we realized that we want to use `:lang`, not `:language`...
(defmulti greeting :lang)
(defmethod greeting "English" [_] "Hello!")

(greeting {:lang "English"})
;=> IllegalArgumentException No method in multimethod 'greeting' for dispatch value: null  clojure.lang.MultiFn.getFn (MultiFn.java:156)


;;  to resolve
(def greeting nil)
; or use ns-unmap
(ns-unmap *ns* 'greeting)

; then re-define
(defmulti greeting :lang)
(defmethod greeting "English" [_] "Hello!")

(greeting {:lang "English"})
;=> Hello!
```
