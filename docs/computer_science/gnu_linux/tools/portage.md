---
title: 'Portage: Gentoo package manager'
date: 2017-12-03
tags: [ 'gentoo', 'portage', 'emerge', 'package', 'manager', 'sources' ]
---

# Portage: Gentoo package manager

## Usage

### Options

#### Ignore errors and continue

Use the option `--keep-going`.

### Add custom ebuild

Copy the **ebuild** file to the corresponding directory, creating it in its
category, in */usr/portage*. Then:

```bash
chown -R portage:portage /usr/local/portage
pushd [new-directory]
repoman manifest
popd
```

[gentoo-wiki](https://wiki.gentoo.org/wiki/Custom_repository#Adding_an_ebuild_to_the_repository)

## Tips

### Upgrading live ebuilds

If you use the version **9999** of an ebuild, it probably means you are
compiling the **master** branch of the source repo each time. Portage doesn't
check for the updates and won't update this packages automatically (because the
version will always be **9999**). The best way to update them is by using a
script. To find the installed packages you can use:

```bash
find /var/db/pkg/ -mindepth 2 -maxdepth 2 -name \*-9999
```

To upgrade all of them, use:

```bash
emerge -1aAv `find /var/db/pkg/ -mindepth 2 -maxdepth 2 -name \*-9999|awk -F \/ '{printf "=%s/%s ", $5, $6}'`
```

* [gentoo forums](https://forums.gentoo.org/viewtopic-t-544575.html)
