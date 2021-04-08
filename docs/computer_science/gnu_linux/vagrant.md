---
title: vagrant
date: 2017-10-17
tags: vagrant,sysadmin,testing,VM
---
# vagrant

## Provisioning

### Shell

```vagrant
  config.vm.provision "shell", inline: "echo hello"
```
[vagrant-doc](https://www.vagrantup.com/docs/provisioning/basic_usage.html)

### Ansible

```vagrant
# This guide is optimized for Vagrant 1.7 and above.
# Although versions 1.6.x should behave very similarly, it is recommended
# to upgrade instead of disabling the requirement below.
Vagrant.require_version ">= 1.7.0"

Vagrant.configure(2) do |config|

  config.vm.box = "debian/stretch64"

  # Disable the new default behavior introduced in Vagrant 1.7, to
  # ensure that all Vagrant machines will use the same SSH key pair.
  # See https://github.com/mitchellh/vagrant/issues/5005
  config.ssh.insert_key = false

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
	ansible.host_key_checking = false
	ansible.extra_vars = { ansible_ssh_user: 'vagrant', testing: true }
  end
end
```

[ansible-doc](https://docs.ansible.com/ansible/latest/guide_vagrant.html)

#### Workflow

First, start the VM (this will automatically deploy the playbook):

`vagrant up`

If you need to check something:

`vagrant ssh`

If you need to re-run the playbook:

`vagrant provision`

To stop and delete the VM:

`vagrant destroy --force`

## Configuration

### Common options

* `ansible.inventory_path = "[path]"`
* ```vagrant
ansible.groups = {
  "web" => ["vm1", "vm2"],
  "db"  => ["vm3"]
}
```


[vagrant-doc](https://www.vagrantup.com/docs/provisioning/ansible_common.html)

## Tips

### Disable synced folder

```vagrant
  config.vm.synced_folder '.', '/vagrant', disabled: true
```

[superuser](https://superuser.com/questions/756758/is-it-possible-to-disable-default-vagrant-synced-folder)
