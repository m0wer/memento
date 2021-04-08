---
title: YAML
date: 20171125
tags: yaml,ansible,syntax
---

# YAML

## Syntax

### Multiline variables

* Folding block (joins multiple lines together by spaces):

```yaml
key: >
	hello
	world!
```

* Literal block (really multiline):

```yaml
key: |
	thing1
	thing2
	anotherthing
```

[stackoverflow](https://stackoverflow.com/questions/40230184/how-to-do-multiline-shell-script-in-ansible)
