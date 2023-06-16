---
layout:   post
title:    "python env"
date:     2023-06-16 12:46:00 +0700
tags:     python env venv pipenv
---

### venv
```sh
# create virtual env at .venv folder
python -m venv .venv

# active
source .venv/bin/activate

# install package into it
python -m pip install <package-name>
python -m pip install -r requirements.txt

# deactive
deactivate
```

### pipenv
```sh
# create & start virtual env
pipenv shell
```
