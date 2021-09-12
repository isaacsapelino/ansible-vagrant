# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|   

  if Vagrant.has_plugin?("vagrant-vbguest") then
    config.vbguest.auto_update = false
  end

  config.vm.define "ansible", primary: true do |ansible|

    # Virtual Box Configuration
    ansible.vm.provider "virtualbox" do |vb|
      # Current CPU usage
      vb.cpus = 1
    
      # Customize the amount of memory on the VM:
      vb.memory = "1024"
      
      # Set VM NAME
      vb.name = "Alpine Ansible"

      # Customize VRAM
      vb.customize ["modifyvm", :id, "--vram", "64"]
    end

    ansible.vm.box = "generic/alpine38"
    ansible.vm.network "private_network", ip: "192.168.20.2",
      virtualbox__intnet: "mynetwork"
      
    ansible.vm.synced_folder "./ansible", "/ansible", owner: "vagrant",
      group: "vagrant", :mount_options => ["dmode=755", "fmode=666"]    
      
    ansible.vm.provision "shell", inline: <<-SHELL
      apk update
      apk add git
      apk add ansible
    SHELL

    ansible.vm.provision "shell", inline: <<-SHELL
      sudo mkdir /etc/ansible
      sudo cp -R /ansible/* /etc/ansible
    SHELL
  end

  config.vm.define "ubuntu" do |server1|

    # Virtual Box Configuration
    server1.vm.provider "virtualbox" do |vb|
      # Current CPU usage
      vb.cpus = 1
    
      # Customize the amount of memory on the VM:
      vb.memory = "1024"

      # Set VM NAME
      vb.name = "Ubuntu Server"
  
      # Customize VRAM
      vb.customize ["modifyvm", :id, "--vram", "64"]
    end

    server1.vm.box = "mmichal/ubuntu20_04"
    server1.vm.network "private_network", ip: "192.168.20.3",
      virtualbox__intnet: "mynetwork"
    
    server1.vm.synced_folder "./data", "/vagrant", owner: "vagrant",
      disabled: true

  end

  config.vm.define "centos" do |server2|

    # Virtual Box Configuration
    server2.vm.provider "virtualbox" do |vb|
      # Current CPU usage
      vb.cpus = 1
    
      # Customize the amount of memory on the VM:
      vb.memory = "1024"

      # Set VM NAME
      vb.name = "CentOS 8 Server"
  
      # Customize VRAM
      vb.customize ["modifyvm", :id, "--vram", "64"]
    end

    server2.vm.box = "centos/8"
    server2.vm.network "private_network", ip: "192.168.20.4",
      virtualbox__intnet: "mynetwork"
    
    server2.vm.synced_folder "./data", "/vagrant", owner: "vagrant",
      disabled: true
  end

  config.vm.define "opensuse" do |server3|

    # Virtual Box Configuration
    server3.vm.provider "virtualbox" do |vb|
      # Current CPU usage
      vb.cpus = 1
    
      # Customize the amount of memory on the VM:
      vb.memory = "1024"

      # Set VM NAME
      vb.name = "OpenSUSE Tumbleweed Server"
  
      # Customize VRAM
      vb.customize ["modifyvm", :id, "--vram", "64"]
    end

    server3.vm.box = "opensuse/Tumbleweed.x86_64"

    server3.vm.network "private_network", ip: "192.168.20.5",
      virtualbox__intnet: "mynetwork"
    
    server3.vm.synced_folder "./data", "/vagrant", owner: "vagrant",
      disabled: true

    server3.vm.provision "shell", inline: <<-SHELL
      zypper -n install rsync
    SHELL
  end
end
