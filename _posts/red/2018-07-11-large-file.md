---
layout: post
title:  "reading large data file"
date:   2018-07-11 23:27:00 +0700
category: red
tags:   rebol file port
---

```rebol
; The /direct refinement opens an unbuffered port.
; This is useful to access files a portion at a time,
; such as when a file is too large to be held in memory.
fp: open/direct %file.txt

; Reading the data with a copy function will move the port's head forward.
; & return none when the port has reached its end
while [data: copy/part fp 100000] [
  ; process with data
]

close fp
```

ref [ports](http://www.rebol.com/docs/core23/rebolcore-14.html#section-8.3)
