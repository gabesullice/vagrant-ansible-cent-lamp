# E3 Vagrant

## Installation

* First, ensure you've met the [requirements](#Requirements)
* Look for the following line in your Vagrantfile. Edit the first path to reflect your project directory.
```ruby
config.vm.synced_folder "~/development/docroot", "/vagrant_data", type: "nfs"
```
* From this repo's directory, spin up the vagrant box
```bash
vagrant up
```
* If the provisioner didn't run, you can run:
```bash
vagrant provision
```
You can run this as often as you like.

### Setting up a site

Setting up local sites is easy. Sites provisionable by ansible should have an ansible directory at the topmost level (next to .git). Instructions for setting up a new local site can be found in the [e3 skel for ansible](https://github.com/elevatedthird/toolbox/tree/master/d7/skel/ansible).

## Requirements

* [Vagrant](http://docs.vagrantup.com/v2/installation/index.html)
* [Ansible](http://docs.ansible.com/intro_installation.html#getting-ansible)
