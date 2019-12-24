# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.define "jupyter" do |jupyter|
    jupyter.vm.box = "centos/7"
    jupyter.vm.hostname = "jupyter"
    jupyter.vm.network "private_network", ip: "192.168.0.10"
  end

  config.vm.define "nginx" do |nginx|
    nginx.vm.box = "centos/7"
    nginx.vm.hostname = "nginx"
    nginx.vm.network "private_network", ip: "192.168.0.20"
    nginx.vm.network "forwarded_port", guest: 443, host: 4443
    nginx.vm.network "forwarded_port", guest: 80, host: 8080
  end

  # Use :ansible or :ansible_local to
  # select the provisioner of your choice
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "main.yml"
    ansible.groups = {
      "jupyer" => ["jupyter"],
      "nginx" => ["nginx"]
    }
  end
end
