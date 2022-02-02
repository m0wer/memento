---
title: python pip
date: 20171026
tags: pip,python,virtualenv,install,uninstall
---

# Usage

## Uninstall a package

`pip uninstall [package]`

[pypa-doc](https://pip.pypa.io/en/stable/reference/pip_uninstall/)

### Uninstall all packages

```bash
pip freeze | xargs pip uninstall -y
```

# Requirements files

## Structure

Define the user dependencies in `setup.py` and use `pip-compile` to generate
a `requirements.txt` file with the latest compatible versions. Then, create
a `requirements-dev.in` file and add:

```
-c requirements.txt
-e file:.

dep1
dep2
...
```

* `-c requirements.txt` will consider the user dependencies and its versions
  but without adding them also to `requirements-dev.txt`. Add with `-c` any
  other requirements files from the project such as `docs/requirements.txt`.
* `-e file:.` will add the local package so that any changes
  would reflect directly in your environment. `file:.` instead of just `.`
  makes the path in the generated `requirements-dev.txt` relative instead of
  absolute.

Use `pip-compile requirements-dev.in` to generate `requirements-dev.txt`.

# pip-tools

[jazzband/pip-tools](https://github.com/jazzband/pip-tools) are a set of tools
to keep your pinned Python dependencies fresh.

## pip-compile

Define dependencies in `setup.py` or `requirements.in` (without specifying
the version of each package) and then set the version to the latest possible
one by running `pip-compile`, which will generate a `requirements.txt` file.

This is useful for having a saved list with the dependencies and their version
that are compatible among them and with your software (you can check it by
running your software's tests for example).

### Development dependencies

You can build a `requirements-dev.txt` file containing the development
dependencies needed only for development purposes and not for the software
user and considering the dependencies
and versions from `requirements.txt` so that only compatible versions are
chosen.

To do so, create a `requirements-dev.in` file containing:

```
-c requirements.txt
somepackage
otherpackage
...
```

And fix the versions with:

```bash
pip-compile requirements-dev.in
```

Which will generate a `requirements-dev.txt` file.

## pip-sync

To keep the locally installed dependencies synced with these files do:

```bash
python -m piptools sync requirements.txt requirements-dev.txt
```

**Only run inside of a virtual environment.**
