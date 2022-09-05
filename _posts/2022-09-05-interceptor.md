---
layout: post
title:  "Interceptors"
date:   2022-09-05 10:25:00 +0700
tags:   clojure interceptor pedestal pattern
---

## Interceptor

Pedestal calls the `:enter` function on the way "in" to handling a request.
It calls the `:leave` function on the way back "out".
This is shown here for a single interceptor:

![](http://pedestal.io/images/guides/interceptors.png)

All the `:enter` functions are called in order.
Each one receives the context map and returns a (possibly modified) context map.
Once all the interceptors have been called, the resulting context map gets passed through the interceptors' `:leave` functions, but in reverse order, as shown here:

![](http://pedestal.io/images/guides/interceptor-stack.png)

```clojure
(require '[exoscale.interceptor :as interceptor])

(def interceptor-A {:name  :A
                    :enter (fn [ctx] (update ctx :a inc))
                    :leave (fn [ctx] (assoc ctx :foo :bar))
                    :error (fn [ctx err] ctx)})

(def interceptor-B {:name  :B
                    :enter (fn [ctx] (update ctx :b inc))
                    :error (fn [ctx err] ctx)})

(def interceptor-C {:name  :C
                    :enter (fn [ctx] (update ctx :c inc))})

;; enter & leave
(interceptor/execute {:a 0 :b 0 :c 0}
                     [interceptor-A
                      interceptor-B
                      interceptor-C])
;=>
{:a   1
 :b   1
 :c   1
 :foo :bar
 :exoscale.interceptor/queue <-()-<
 :exoscale.interceptor/stack ()}
```

## The Queue and the Stack

Pedestal keeps a queue of interceptors that still need to have their `:enter` functions called.
There is also a stack of interceptors whose `:enter` functions have been called, but their `:leave` functions have not.
As such, the `:leave` functions are called in reverse order to the `:enter` functions.

Suppose we start with three interceptors in the queue, like this:

![](http://pedestal.io/images/guides/what-is-an-interceptor/interceptor-queue-and-stack-in-context-1.png)

Pedestal needs to call the `:enter` function on "Intc 1".
So it pops that interceptor from the queue and moves it to the stack.
Then it calls the interceptor, passing the context map itself.
This is the context as it appears to "Intc 1":

![](http://pedestal.io/images/guides/what-is-an-interceptor/interceptor-queue-and-stack-in-context-2.png)

When that’s done, the next thing is to call "Intc 2".
Same thing happens, Pedestal pops that interceptor from the queue and pushes it on the stack:

![](http://pedestal.io/images/guides/what-is-an-interceptor/interceptor-queue-and-stack-in-context-3.png)

Repeat the process for "Intc 3" and we’re left with this context map:

![](http://pedestal.io/images/guides/what-is-an-interceptor/interceptor-queue-and-stack-in-context-4.png)


## Manipulating the Queue

Both the queue and the stack reside in the context map.
Since interceptors can modify the context map, that means they can change the plan of execution for the rest of the request!

Interceptors are allowed to `enqueue` more interceptors to be called, or they can `terminate` the request.

An example where we dynamically decide which interceptor to add, depending on a query parameter:

```clojure
(def odds {:name  ::odds
           :enter (fn [ctx] (assoc ctx :msg "I handle odd number"))})

(def evens {:name  ::evens
            :enter (fn [ctx] (assoc ctx :msg "Even numbers are my bag"))})

(def chooser
  {:name  ::chooser
   :enter (fn [ctx]
              (let [n (:n ctx)
                    nxt (if (even? n) evens odds)]
                   (interceptor/enqueue ctx [nxt])))})


(interceptor/execute {:n 0} [chooser])
;=>
{:n 0,
 :msg "Even numbers are my bag"}

(interceptor/execute {:n 1} [chooser])
;=>
{:n 1,
 :msg "I handle odd number"}
```

### Interceptors or Middleware

Middleware models wrap up the whole processing chain in function closures.
Not only are they opaque, but the decisions are all made at compile time.

In contrast, Pedestal treats the processing chain like a virtual call stack, or a malleable program to execute.


## Error Handling

The `:error` function is a bit special.

If an interceptor throws an exception, then Pedestal starts looking for an interceptor with an `:error` function to handle it.
This goes from right-to-left like the `:leave` functions.

The main difference is that an error-handling interceptor may indicate that the error is totally resolved and Pedestal will resume looking for `:leave` functions.

```clojure
(def interceptor-A {:name  :A
                    :enter (fn [ctx] (update ctx :a inc))
                    :leave (fn [ctx] (assoc ctx :foo :bar))
                    :error (fn [ctx err] ctx)})

(def interceptor-B {:name  :B
                    :enter (fn [ctx] (update ctx :b #(Integer/parseInt %)))
                    :error (fn [ctx err]
                               (if (instance? java.lang.NumberFormatException err)
                                 (assoc ctx :msg ":b isn't a number!")
                                 (assoc ctx ::interceptor/error err)))})

(def interceptor-C {:name  :C
                    :enter (fn [ctx] (update ctx :c inc))})


; in case we got NumberFormatException on interceptor-B
; interceptor-C is not executed
; :error on intercepter-B is executed & return a context map. So next :leave on interceptor-A is call.
(interceptor/execute {:a 0 :b "x" :c 0}
                     [interceptor-A
                      interceptor-B
                      interceptor-C])
;=>
{:a 1,
 :b "x",
 :c 0,
 :msg ":b isn't a number!",
 :foo :bar}


; in case we got ClassCastException on interceptor-B
; interceptor-C is not executed
; :error on intercepter-B is executed & add ::error to context map. So next :error on interceptor-A is call instead of :leave
(interceptor/execute {:a 0 :b 0 :c 0}
                     [interceptor-A
                      interceptor-B
                      interceptor-C])
;=>
{:a 1,
 :b 0,
 :c 0}
```


## Async


## Ref 

- http://pedestal.io/reference/interceptors
- http://pedestal.io/guides/what-is-an-interceptor
- https://github.com/exoscale/interceptor