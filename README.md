# E3 Vagrant

## Installation

1. First, ensure you've met the [requirements](#Requirements)
2. Look for the following line in your Vagrantfile. Edit the first path to reflect your project directory.
```ruby
config.vm.synced_folder "~/development/docroot", "/vagrant_data", type: "nfs"
```
3. From this repo's directory, spin up the vagrant box
```bash
vagrant up
```

## Requirements

* [Vagrant](http://docs.vagrantup.com/v2/installation/index.html)
* [Ansible](http://docs.ansible.com/intro_installation.html#getting-ansible)
