# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 256
    # vb.linked_clone = true
  end 

  config.vm.provision "shell",
    inline: "apt-get update"

  
  config.vm.define "web" do |web|
    web.vm.network "forwarded_port", guest: 80, host: 8080
    web.vm.network "private_network", ip: "192.168.57.10"
    web.vm.synced_folder "./web", "/var/www/html"
    web.vm.provision "shell", inline: <<-SHELL
    apt-get install -y apache2
    cp -v /vagrant/web/index.html /var/ww/html
    SHELL
   
  end # web

  config.vm.define "bd" do |bd|
    bd.vm.box = "ubuntu/trusty64"
  end # bd

end
