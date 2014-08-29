# E3 Vagrant

## Installation

1. First, ensure you've met the [requirements](#requirements)
2. Copy the `local.yml.example` file to `local.yml`. This file contains all settings unique to your local machine and is ignored by Git.
3. Update the settings to match your local setup.
4. From this repo's directory, spin up the vagrant box
```bash
vagrant up
```
5. If the provisioner didn't run, you can run the following. You can run this as often as you'd like.
```bash
vagrant provision
```
6. Finally, for our other ansible playbooks to run, you will need to add this vagrant instance as an andible host. If `/usr/local/etc/hosts/ansible/hosts` does not already exist. Create it.
```bash
sudo mkdir /usr/local/etc/ansible
sudo touch /usr/local/etc/ansible/hosts
```
7. With that files in place, add the following to it.
```
[vagrant]
192.168.33.10
```

### Setting up a new site on your vagrant instance

Setting up local sites is easy. Sites provisionable by ansible should have an ansible directory at the topmost level (next to .git). Instructions for setting up a new local site can be found in the [e3 skel for ansible](https://github.com/elevatedthird/toolbox/tree/master/d7/skel/ansible).

## Requirements

* [Vagrant](http://docs.vagrantup.com/v2/installation/index.html)
* [Ansible](http://docs.ansible.com/intro_installation.html#getting-ansible)
