---
layout:   post
title:    "transducer"
date:     2018-07-15 11:23:00 +0700
category: clojure
tags:     clojure transducer
---

```clj
;; inside understand
; http://elbenshira.com/blog/understanding-transducers/

; reducing fn: result, input -> result
(conj [1 2 3] 4)
;=> [1 2 3 4]

(+ 10 1)
;=> 11

; transducer (xform): transform from one reducing fn to another
; (result, input -> result) -> (result, input -> result)


;; how to use
; https://clojure.org/reference/transducers
; https://www.astrecipes.net/blog/2016/11/24/transducers-how-to/

(filter odd?) ;; returns a transducer that filters odd
(map inc)     ;; returns a mapping transducer for incrementing
(take 5)      ;; returns a transducer that will take the first 5 values

; comp: right-to-left, but builds a transformation stack runs left-to-right ~ thread macro
(def xf
  (comp
    (filter odd?)
    (map inc)
    (take 5)))

; equivalent
(->> coll
     (filter odd?)
     (map inc)
     (take 5))


;; transduce will immediately (not lazily) reduce over coll
;; with the transducer xform applied to the reducing function f
(transduce xform f coll)
(transduce xform f init coll)

(def xf (comp (filter odd?) (map inc)))
(transduce xf + (range 5))
;=> 6
(transduce xf + 100 (range 5))
;=> 106


;; eduction returns a reducible/iterable
(def iter (eduction xf (range 5)))
(reduce + 0 iter)
;=> 6


;; into: transducer coll -> coll
(into [] xf (range 1000))

(sequence xf (range 1000))


;; creating transducers
; https://dev.to/greencoder/build-your-own-transducer-and-impress-your-cat---part-1-mhp
(fn [xf]
  (fn ([] ...)                ; init
      ([result] ...)          ; completion
      ([result input] ...)))  ; step

(def inc-transducer
  (fn [rf]
    (fn ([] (rf))                                   ; 0-arity aka 'the useless'
        ([result] (rf result))                      ; 1-arity aka 'the flusher'
        ([result input] (rf result (inc input)))))) ; 2-arity aka 'the doer'

(into [] inc-transducer (list 4 5 6))
; => [5 6 7]
; idiomatic way:
; (into [] (map inc) (list 4 5 6))


;; with core.async
; https://eli.thegreenplace.net/2017/reducers-transducers-and-coreasync-in-clojure/
; https://malcolmsparks.com/posts/transducers.html
```
