# E3 Vagrant

## Installation

1. First, ensure you've met the [requirements](#Requirements)
1. Look for the following line in your Vagrantfile. Edit it to reflect your projects directory.
```ruby
config.vm.synced_folder "~/development/docroot", "/vagrant_data", type: "nfs"
```

## Requirements

* [Vagrant](http://docs.vagrantup.com/v2/installation/index.html)
* [Ansible](http://docs.ansible.com/intro_installation.html#getting-ansible)
