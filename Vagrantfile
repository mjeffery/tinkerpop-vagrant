# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/vivid64"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine.
  config.vm.network "forwarded_port", guest: 5000, host: 5000

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.

  # config.vm.network "public_network"
  config.vm.synced_folder "app/", "/home/vagrant/flask-server/"

  # Enable provisioning with a shell script.
  config.vm.provision "shell", inline: <<-SHELL
    cp /vagrant/vimrc ~/.vimrc
    debconf-set-selections <<< 'mysql-server mysql-server/root_password password pw4root'
    debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password pw4root'
    sudo apt-get update
    sudo apt-get install -y python-virtualenv
    sudo apt-get install -y mysql-server
    cd flask-server
    virtualenv venv --always-copy ; . venv/bin/activate
    easy_install -U pip
    pip install Flask
    pip install SQLalchemy
  SHELL
end
