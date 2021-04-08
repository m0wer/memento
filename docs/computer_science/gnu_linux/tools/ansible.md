---
title: Ansible
date: 2017-10-12
tags: [ 'ansible', 'sysadmin', 'automation', 'ssh', 'remote' ]
---

# Ansible

## Usage

### Meta

Run handlers (before): `- meta: flush_handlers`

[ansible handlers](http://docs.ansible.com/ansible/playbooks_intro.html#handlers-running-operations-on-change)

### Loops

#### Looping over Subelements

Useful when you have a list of dictionaries and you want to pick the same
element from all of them.

```yaml
with_subelements:
  - "{{ some list }}"
  - interesting_list_item
  - flags:
    skip_missing: yes
```

[ansible-docs](https://docs.ansible.com/ansible/latest/playbooks_loops.html#looping-over-subelements)

### Command line

#### Variables

To provide variables directly from the command line:
`--extra-vars "version=1.23.45 other_variable=foo"`.

[stackoverflow](https://stackoverflow.com/questions/30662069/how-can-i-pass-variable-to-ansible-playbook-in-the-command-line)

### Facts

* `ansible_user_id`

#### Only gather facts when tag matches

To speed up playbooks, disable `gather_facts`. In the parts where this is
requiered, you can use this approach:

```yaml
- hosts: all
  sudo: yes
  gather_facts: False
  pre_tasks:
   - setup:
       filter: ansible_*
  roles:
   - your_role_here
  tags:
    - tag1
```

This way ansible will only gather some facts and only if the tag matches (when
run with the `-t` option).

[stackoverflow](https://stackoverflow.com/questions/34485286/ansible-gathering-facts-with-filter-inside-a-playbook#34487639)

## Debug

### Include tags ignored

Example:

```yaml
- import_tasks: db-setup.yml tags=db-setup
```

This tags are ignored if you skip them. Bug: [github](https://github.com/ansible/ansible/issues/9862)

### could not find `item['foo']` key in iterated item

Solution: specify a third element in the **with_subelements** list called
**flags** that is a dict and contains **skip_missing: yes**.

```yaml
with_subelements:
  - "{{ some list }}"
  - interesting_list_item
  - flags:
    skip_missing: yes
```

[github-issues](https://github.com/ansible/ansible/pull/10995)

## Reference

### Usage

* [ansible-docs](https://ansible-docs.readthedocs.io/zh/stable-2.0/rst/playbooks_filters.html)
  Jinja2 filters.

### Modules

* [mysql_db](https://docs.ansible.com/ansible/latest/mysql_db_module.html)
* [docker_container](https://docs.ansible.com/ansible/latest/docker_container_module.html)

### Utilities

* [ansigenome](https://github.com/nickjj/ansigenome) Tool for calculating
   dependency graphs and more.

### Vault

* [serversforhackers](https://serversforhackers.com/c/how-ansible-vault-works)

### Plugins

#### Timing

Displays tasks timing at the end of the playbook output.

To enable, add `callback_whitelist = profile_tasks` to *ansible.cfg*.

[ansible-profile](https://github.com/jlafon/ansible-profile)
