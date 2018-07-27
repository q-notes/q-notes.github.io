---
layout: post
title:  "tmux/screen"
date:   2018-06-22 15:19:00 +0700
tags:   linux tmux screen
---

|                | tmux                         | screen |
| -------------- | ---------------------------- | ------ |
| new session    | `tmux`                       | `screen` |
| list session   | `tmux ls`                    | `screen -ls` |
| attach session | `tmux a -t <id>`             | `screen -r <id>` |
| detach session | `ctrl + b, d`                | `ctrl + a, d` |
| kill sesion    | `tmux kill-session -t <id>`  | `ctrl + a, k` (on session) |
| scroll         | `ctrl + b, [`<br/>q for quit | `ctrl + a, Esc`<br/>q for quit |
