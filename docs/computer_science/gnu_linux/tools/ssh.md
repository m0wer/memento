---
title: SSH
date: 2018-10-27
tags: [ 'ssh', 'usage', 'remote', 'connection', 'tips' ]
---

# SSH

## Usage

### Connecting

#### Force password login

`ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no [host]`

[unix-stack_echange](https://unix.stackexchange.com/questions/15138/how-to-force-ssh-client-to-use-only-password-auth)

#### Jumping through a host

`ssh -J [host1] [host2]`

[wiki-gentoo](https://wiki.gentoo.org/wiki/SSH_jump_host)

### SSH tunneling

#### Make Remote Resources Accessible on Your Local System

```bash
ssh -L local_port:remote_address:remote_port username@server.com
```

* [howtogeek](https://www.howtogeek.com/168145/how-to-use-ssh-tunneling/)

## Config

### Multiple similar entries

If you have multiple similar entries, they can share the common part:

```
Host X01
    HostName X01.YYY.com

Host X02
    HostName X02.YYY.com

...

Host X01 X02 ...
     User my_username
     Compression yes
     Ciphers arcfour,blowfish-cbc
     Protocol 2
     ControlMaster auto
     ControlPath ~/.ssh/%r@%h:%p
     IdentityFile ~/.ssh/YYY/id_rsa
```

[stackexchange](https://unix.stackexchange.com/questions/61655/multiple-similar-entries-in-ssh-config)

### Conflicting remote host keys on the same IP

If you have different servers that use the same IP (at different times maybe),
you'll have some annoying security alerts about their keys not matching with
the previously stored one (since you only can save one of them). What you can
do without risking the connection security is adding thes hosts like this in
your *~/.ssh/config*:

```
Host server1
  Hostname x1.example.com
  HostKeyAlias server1
  CheckHostIP no
  Port 22001
  User karl

Host server2
  Hostname x2.example.com
  HostKeyAlias server2
  CheckHostIP no
  Port 22002
  User karl
```

The important part is the **HostKeyAlias** line, that allows the SSH client to
store the remote server public keys with the alias instead of with the unique
shared IP address.

[stackoverflow](https://stackoverflow.com/questions/733753/how-to-handle-ssh-host-key-verification-with-2-different-hosts-on-the-same-but)

### Dynamic IP host verification

When you have a dynamic IP host, you might get `Warning: the [whatever] host
key for '[host]' differs from the key for the IP address` that is true, but
also pretty annoying. If you'd rather just verify a host by its keys, instead
of keys+IP, try with:

```
Host nickname
   HostName example.dynamic.tld
   CheckHostIP no
```

* [askubuntu](https://askubuntu.com/questions/48317/trust-ssh-server-based-on-key-instead-of-if-keyip-match)

## Debug

### Ctrl+s hangs the terminal

From **vimdoc**:

```
Note: CTRL-S does not work on all terminals and might block
                further input, use CTRL-Q to get going again.
```

[stackexchange](https://unix.stackexchange.com/questions/72086/ctrl-s-hang-terminal-emulator)
