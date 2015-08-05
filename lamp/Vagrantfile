# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "lamp-stack"

  config.vm.network "forwarded_port", guest: 80, host: 8000
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"
  config.ssh.forward_agent = true
  #config.vm.synced_folder ".", "/home/vagrant", :owner=> "vagrant", :group=> "www-data", :mount_options => ['dmode=775', 'fmode=775']
  config.vm.synced_folder ".", "/home/vagrant/www"
  # config.vm.provider "virtualbox" do |vb|
  #   # Don't boot with headless mode
  #   vb.gui = true
  #
  #   # Use VBoxManage to customize the VM. For example to change memory:
  #   vb.customize ["modifyvm", :id, "--memory", "1024"]
  # end
  config.vm.provision "file", source: "001-lamp.conf", destination: "/tmp/001-lamp.conf"
  config.vm.provision "file", source: "lamp_database.sql", destination: "/tmp/lamp_database.sql"
  config.vm.provision "shell", path: "./provisioner"
  config.vm.provision "shell", inline: "sudo service apache2 start", run: "always"
end
