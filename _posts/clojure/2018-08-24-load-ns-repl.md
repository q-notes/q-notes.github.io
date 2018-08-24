---
layout:   post
title:    "load ns on repl"
date:     2018-08-24 23:05:00 +0700
category: clojure
tags:     clojure repl ns
---

```clj
$ clj
Clojure 1.9.0
user=> (load "clj_todo_list/handler")
nil
user=> (in-ns 'clj-todo-list.handler)
```
