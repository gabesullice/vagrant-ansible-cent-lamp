# E3 Vagrant

## Installation

After cloning this repo, you will need to make a minor configuration change.

1. [Install Vagrant](http://docs.vagrantup.com/v2/installation/index.html)
1. [Install Ansible](http://docs.ansible.com/intro_installation.html#getting-ansible)
1. Look for the following line in your Vagrantfile. Edit it to reflect your projects directory.
```ruby
config.vm.synced_folder "~/development/docroot", "/vagrant_data", type: "nfs"
```
