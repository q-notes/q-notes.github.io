---
layout: post
title:  "http static server one-liners"
date:   2018-06-22 22:15:00 +0700
tags:   web http one-liners
---

+ Python 2
```sh
$ python -m SimpleHTTPServer 8000
```

+ Python 3
```sh
$ python -m http.server 8000
```

+ Node.js
```sh
$ npm install -g http-server   # install dependency
$ http-server -p 8000
```

+ ngrok
```sh
$ ./ngrok http 8000
```
