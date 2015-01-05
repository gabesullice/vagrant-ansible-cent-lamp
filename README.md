# E3 Vagrant

## Installation

* First, ensure you've met the [requirements](#requirements)
* Copy the `local.yml.example` file to `local.yml`. This file contains all settings unique to your local machine and is ignored by Git.
* Update the settings to match your local setup.
* From this repo's directory, spin up the vagrant box
```bash
vagrant up
```
* If the provisioner didn't run, you can run the following. You can run this as often as you'd like.
```bash
vagrant provision
```
* Finally, for our other ansible playbooks to run, you will need to add this vagrant instance as an ansible host. If `/usr/local/etc/hosts/ansible/hosts` does not already exist. Create it.
```bash
sudo mkdir /usr/local/etc/ansible
sudo touch /usr/local/etc/ansible/hosts
```
* With that file in place, add the following to it.
```
[vagrant]
192.168.50.50
```

### Setting up a new site on your vagrant instance

Setting up local sites is easy. Sites provisionable by ansible should have an ansible directory at the topmost level (next to .git). Instructions for setting up a new local site can be found in the [e3 skel for ansible](https://github.com/elevatedthird/toolbox/tree/master/d7/skel/ansible).

### Interacting with Vagrant databases

You can interact with databases hosted on Vagrant using a tool like [Sequel Pro](http://www.sequelpro.com/). The documented steps are for Sequel Pro, however they should be similar for your specific tool.

* Click on the "SSH" tab.
* Provide the credentials:
  * MySQL Host: 127.0.0.1
  * Username: root
  * Password: \<leave empty>
  * Database: \<leave empty>
  * Port: \<leave empty>
  * SSH Host: 192.168.50.50
  * SSH User: vagrant
  * SSH Key: \<leave empty. See note below if you experience issues>
  * SSH Port: \<leave empty>

\* Typically, this can be left blank. Sequel Pro is set up to find either your computer's pubkey or Vagrant's. Your computer's key is typically found at `~/.ssh/id_rsa`. Vagrant's is typically `~/.vagrant.d/insecure_private_key`. Depending on your own setup, your own paths may be different and you should change this field accordingly.

#### <a id="ssh-keys"></a> SSH Keys

Our Ansible playbook will add your pubkey at ~/.ssh/id_rsa.pub to the vagrant guest's authorized_keys file by default. This means you can ssh into vagrant with `ssh 192.168.33.10` from any directory as you would any other remote server. For ease of use, you can enable defaults for this SSH connection by adding the following to ~/.ssh/config. Then, you can simply use `sss vagrant` as a handy shorthand.

```
Host vagrant
  HostName 192.168.50.50
  ForwardAgent yes
  User vagrant
  IdentityFile ~/.ssh/id_rsa
```

## Requirements

* [Vagrant](http://docs.vagrantup.com/v2/installation/index.html)
* [Ansible](http://docs.ansible.com/intro_installation.html#getting-ansible)
