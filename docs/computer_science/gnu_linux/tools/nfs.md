---
title: NFS
date: 2018-11-25
tags: [ 'linux', 'gnu', 'nfs', 'network', 'filesystem' ]
---

# NFS

## Usage

### NFSv4

#### Server

In */etc/exports*:

```
/export       192.168.1.0/24(rw,fsid=0,no_subtree_check)
```

And then you can add other directories that are inside */export* in the server.
NFSv4 NFSv4 dictates that the additional shared directories are subdirectories
of the root share (the one with `fsid=0`).

#### Client

```bash
mount -t nfs4 -o proto=tcp,port=2049 [nfs-server]:/ /mnt
```

**Note**: Yo should specify the path relative to the root share folder.

##### /etc/fstab

```
Server:/path/to/export /local_mountpoint nfs hard,intr 0 0
```

* [Linux NFS Mount Entry in fstab ( /etc/fstab ) with Example](https://linoxide.com/file-system/example-linux-nfs-mount-entry-in-fstab-etcfstab/)

## Debug

From the client try:

```bash
mount -v -o nfsvers=4 [nfs-server]:/ /mnt
```

## Reference

### NFSv4

* [ubunut-help](https://help.ubuntu.com/community/NFSv4Howto)
