---
layout: post
title:  supervisord
date:   2018-06-28 11:54:00 +0700
category: linux
tags:   linux devops supervisord
---

+ Reloading configuration changes

```sh
# restart application without making configuration changes available
$ supervisorctl restart <name>

# load config changes, but don't restart apps
$ supervisorctl reread

# restarts the applications with config changes
$ supervisorctl update
```
