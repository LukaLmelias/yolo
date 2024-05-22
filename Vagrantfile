# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  
  #define the OS for all the vms
  config.vm.box = "geerlingguy/ubuntu2004"
  #disable key checks
  #config.ssh.insert_key = false
  

  #mongo db vm
  config.vm.define "mongodb" do |mongodb|

    #mongodb.vm.box = "geerlingguy/ubuntu2004"

  # forwad port for other containers to access
    mongodb.vm.network "forwarded_port", guest: 27017, host: 27017, host_ip: "127.0.0.1"
  end


  #backend vm
  config.vm.define "backend" do |backend|
    #backend.vm.box = "geerlingguy/ubuntu2004"

  # forwad port for other containers to access
    backend.vm.network "forwarded_port", guest: 5000, host: 5000, host_ip: "127.0.0.1"
  end


  #client vm
  config.vm.define "client" do |client|
    #client.vm.box = "geerlingguy/ubuntu2004"

  # forwad port for other containers to access
    client.vm.network "forwarded_port", guest: 3000, host: 3000, host_ip: "127.0.0.1"
  end

  # Ansible provisioner for all hosts
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml" # Path to your playbook
    ansible.inventory_path = "hosts" # Path to your inventory file
    
  end

  
end
