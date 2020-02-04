---
layout: post
title:  "stack & queue"
date:   2018-07-03 21:51:00 +0700
tags:   algorithms stack queue clojure java red janet
---

### Stack
- Java

```java
Stack<Integer> st = new Stack<>();

st.push(1); // st=[1]
st.push(2); // st=[1, 2]
st.push(3); // st=[1, 2, 3]

// returns the element on the top of the stack, removing it from stack
st.pop(); //=> 3, st=[1, 2]

// returns the element on the top of the stack, but does not remove it
st.peek(); //=> 2, st=[1, 2]
```

- Clojure Vector

```clj
(def st [1 2 3])
; the functions operate on the right side
(peek st)   ;=> 3
(pop st)    ;=> [1 2]
(conj st 4) ;=> [1 2 3 4]
```

- Clojure List

```clj
(def st '(1 2 3))
; the functions operate on the left side
(peek st)   ;=> 1
(pop st)    ;=> (2 3)
(conj st 4) ;=> (4 1 2 3)
```

### Queue

Add last, remove first impl:

+ Java

```java
Queue<Integer> q = new LinkedList<>();

q.addLast(1); // q=[1]
q.addLast(2); // q=[1, 2]
q.addLast(3); // q=[1, 2, 3]

q.poll(); //=> 1, q=[2, 3]

q.peek(); //=> 2, q=[2, 3]
```

+ Clojure

```clj
(def q (conj PersistentQueue/EMPTY 1 2 3))

(peek q)   ;=> 1
(pop q)    ;=> <-(2 3)-<
(conj q 4) ;=> <-(1 2 3 4)-<
```
