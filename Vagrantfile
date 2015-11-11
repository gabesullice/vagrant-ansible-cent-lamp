# -*- mode: ruby -*-
# vi: set ft=ruby :
require 'yaml'

# Check if the local settings file exists and load the variables from there. If
# it's not found we set some defaults.
if File.exist?('local.yml')
  localSettings = YAML.load_file('local.yml')
else
  localSettings['synced_folder'] = "~/Sites" # Mac assumptions
end

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "atenstd" do |atenstd|
    config.vm.box = "ubuntu/trusty64"

    config.vm.hostname = "atenstd"

    # Create a private network, which allows host-only access to the machine
    # using a specific IP.
    config.vm.network "private_network", ip: "192.168.50.55"

    config.ssh.forward_agent = true
    config.vm.synced_folder localSettings['synced_folder'], "/var/www", type: "nfs"

    # config.vm.box_check_update = false
    # config.vm.network "forwarded_port", guest: 80, host: 8080
    # config.vm.network "public_network"

    config.vm.provider "virtualbox" do |vb|
      host = RbConfig::CONFIG['host_os']

      # Give VM 1/4 system memory & access to all cpu cores on the host
      if host =~ /darwin/
        # sysctl returns Bytes and we need to convert to MB
        mem = `sysctl -n hw.memsize`.to_i / 1024 / 1024 / 4
      elsif host =~ /linux/
        # meminfo shows KB and we need to convert to MB
        mem = `grep 'MemTotal' /proc/meminfo | sed -e 's/MemTotal://' -e 's/ kB//'`.to_i / 1024 / 4
      else # sorry Windows folks, I can't help you
        mem = 1024
      end

      vb.customize ["modifyvm", :id, "--memory", mem]
      vb.customize ["modifyvm", :id, "--cpus", "1"]
    end

    #config.vm.provision "ansible" do |ansible|
    #  ansible.playbook = "provision/main.yml"
    #  ansible.limit = "vagrant"
    #  ansible.skip_tags = ["aten"]
    #  ansible.groups = {
    #    "vagrant" => ["atenstd"],
    #  }
    #end

  end
end
