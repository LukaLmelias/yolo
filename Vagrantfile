# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  
  
  #mongo db vm
  config.vm.define "yolo-mongodb" do |yolo-mongodb|

    yolo-mongodb.vm.box = "geerlingguy/ubuntu2004"

  # forwad port for other containers to access
    yolo-mongodb.vm.network "forwarded_port", guest: 27017, host: 27017, host_ip: "127.0.0.1"
  end


  #backend vm
  config.vm.define "yolo-backend" do |yolo-backend|
    yolo-backend.vm.box = "geerlingguy/ubuntu2004"

  # forwad port for other containers to access
    yolo-backend.vm.network "forwarded_port", guest: 5000, host: 5000, host_ip: "127.0.0.1"
  end


  #client vm
  config.vm.define "yolo-client" do |yolo-client|
    yolo-client.vm.box = "geerlingguy/ubuntu2004"

  # forwad port for other containers to access
    yolo-client.vm.network "forwarded_port", guest: 5000, host: 5000, host_ip: "127.0.0.1"
  end

  
end
