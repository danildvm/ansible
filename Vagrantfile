# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.define "web" do |web|
    web.vm.box = "centos/7"
    ENV['LC_ALL']="en_US.UTF-8"
    web.vm.hostname = "web"
    web.vm.network "forwarded_port", guest: 80, host: 8081
    web.vm.network :private_network, ip: "192.168.0.200"
    config.vm.provider "virtualbox" do |vb|
       vb.gui = false
      vb.memory = "512"
      vb.name = "web"
    end

    web.vm.provision "ansible" do |ansible|
      ansible.playbook = "web.yml"
      ansible.inventory_path = "inventory"
      ansible.become = true
#      ansible.verbose = "vv"
    end
  end

  config.vm.define "mysql" do |mysql|
    mysql.vm.box = "centos/7"
    ENV['LC_ALL']="en_US.UTF-8"
    mysql.vm.hostname = "mysql"
    mysql.vm.network "forwarded_port", guest: 3306, host: 3306
    mysql.vm.network :private_network, ip: "192.168.0.201"
    mysql.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = "512"
        vb.name = "mysql"
    end
    mysql.vm.provision "ansible" do |ansible|
        ansible.playbook = "mysql.yml"
        ansible.inventory_path = "inventory"
        ansible.become = true
#        ansible.verbose = "vv"
    end
  end
end