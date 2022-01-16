---
layout: post
title:  "Install Java"
date:   2020-06-09 10:25:00 +0700
tags:   java
---

- download openjdk & unzip to `/Library/Java/JavaVirtualMachines/` dir

```sh
alias j8="export JAVA_HOME=`/usr/libexec/java_home -v 1.8`; java -version"
alias j13="export JAVA_HOME=`/usr/libexec/java_home -v 13`; java -version"
```
