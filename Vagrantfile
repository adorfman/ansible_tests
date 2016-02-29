# -*- mode: ruby -*-
# vi: set ft=ruby :

# All boxes based off https://github.com/2creatives/vagrant-centos/releases/download/v6.4.2/centos64-x86_64-20140116.box
Vagrant.configure(2) do |config|

  config.vm.provision "shell", inline: "echo whatsup"

  config.ssh.insert_key    = false
  config.ssh.forward_agent = true

  config.vm.synced_folder ".", "/vagrant", :mount_options => [ "dmode=777","fmode=666" ]

  config.vm.define "lb" do |web|
    web.vm.box = "centos65-x86_64-20140116"

    web.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      vb.gui = false 
  
      # Customize the amount of memory on the VM:
      vb.memory = "512"
    end

    web.vm.network "private_network", ip: "192.168.100.8"
    web.vm.hostname = "lb"
    web.vm.provision :hosts, :sync_hosts => true

  end

  config.vm.define "webone" do |web|
    web.vm.box = "centos65-x86_64-20140116"

    web.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      vb.gui = false 
  
      # Customize the amount of memory on the VM:
      vb.memory = "512"
    end

    web.vm.network "private_network", ip: "192.168.100.10"
    web.vm.hostname = "web1"
    web.vm.provision :hosts, :sync_hosts => true

  end

  config.vm.define "webtwo" do |web|
    web.vm.box = "centos65-x86_64-20140116"

    web.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      vb.gui = false 
  
      # Customize the amount of memory on the VM:
      vb.memory = "512"
    end

    web.vm.network "private_network", ip: "192.168.100.12"
    web.vm.hostname = "web2"
    web.vm.provision :hosts, :sync_hosts => true

  end

  config.vm.define "db" do |db|
    db.vm.box = "centos65-x86_64-20140116"

    db.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      vb.gui = false 
  
      # Customize the amount of memory on the VM:
      vb.memory = "512"
    end

    db.vm.network "private_network", ip: "192.168.100.11"
    db.vm.hostname = "db1"
    db.vm.provision :hosts, :sync_hosts => true

  end

  config.vm.define "core" do |core|
    core.vm.box = "centos65-x86_64-20140116"

    core.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      vb.gui = false 
  
      # Customize the amount of memory on the VM:
      vb.memory = "512"
    end

    core.vm.network "private_network", ip: "192.168.100.5"
    core.vm.hostname = "core1"
    core.vm.provision :hosts, :sync_hosts => true

    # Theres a bug in =< 1.8.1 that breaks some actions in this, 
    # its supposed to be fixed in the next point release 
    # Destroy broken https://github.com/mitchellh/vagrant/issues/6763
    # provision broken https://github.com/mitchellh/vagrant/issues/6757
    # For now I guess just comment it out when doing destroy
    # and manually log into core and run ansible 
    core.vm.provision :ansible_local do |ansible|
      ansible.playbook          = "site.yml"
      ansible.verbose           = true
      ansible.install           = true
      ansible.limit             = "all" # or only "nodes" group, etc.
      ansible.inventory_path    = "inventory"
      ansible.provisioning_path = "/vagrant/ansible_testing"
    end

  end

end
