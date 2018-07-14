---
layout: post
title:  "console input & output"
date:   2018-07-12 17:20:00 +0700
tags:   red clojure ruby console cli command-line-args
---

|   | Clojure | Red | Ruby |
| - | ------- | --- | ---- |
| output  | `print` `println`<br/>`pr` `prn`  | `prin` `print`<br/>`probe`  | `print` `puts`<br/>`p` |
| input  | (println (read-line))  | name: input<br/>print name<br/><br/>name: ask "What is your name: "<br/>print name | line = gets<br/>puts line  |
| cmd-line args  | (pr \*command-line-args\*)<br/><br/>$ clj args.clj cat dog<br/>("cat" "dog") | probe system/script/args<br/><br/>$ red args.red 78 A Red<br/>"78 A Red" | p ARGV<br/><br/>$ ruby args.rb cat dog<br/>["ant", "bee", "cat", "dog"]  |
