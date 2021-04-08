---
title: virtualenvwrapper
date: 2017-10-26
tags: [ 'pip', 'python', 'virtualenv', 'utility' ]
---

# virtualenvwrapper

## Usage

### Create a virtualenv

```bash
mkvirtualenv --python `which python2` [name]
```

### Switch between virtualenvs

`workon [name]`

## Install

```bash
export WORKON_HOME=~/Envs
mkdir -p $WORKON_HOME
source /usr/local/bin/virtualenvwrapper.sh
```

[virtualenvwrapper-doc](https://virtualenvwrapper.readthedocs.io/en/latest/)

## Config

### Setup enviroment variables in a virtualenv

Edit *$VIRTUAL_ENV/bin/postactivate* and there add:

```bash
export VAR=value
```

[stackoverflow](https://stackoverflow.com/questions/9554087/setting-an-environment-variable-in-virtualenv)
