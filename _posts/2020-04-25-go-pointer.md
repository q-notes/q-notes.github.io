---
layout: post
title:  "Go Pointers"
date:   2020-04-25 10:25:00 +0700
tags:   golang 
---

A pointer holds the memory address of a value.

```go
// pointer types
var p *int

// The & operator generates a pointer to its operand.
i := 42
p = &i

// The * operator denotes the pointer's underlying value (deref).
fmt.Println(*p) // read i through the pointer p
*p = 21         // set i through the pointer p
```
