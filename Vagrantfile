# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.define "dairyd-buster64"
  config.vm.box = "debian/buster64"
  config.vm.hostname = "dairyd-buster64.local"
  config.vm.boot_timeout = 600
  config.vm.box_check_update = false
  config.vm.network "public_network"
  config.vm.provider "virtualbox" do |vb|
     vb.memory = "2048"
     vb.name = "dairyd-buster64"
  end

  config.vm.provision "shell", inline: <<-SHELL
      echo "dairyd"
      echo "============================================"
      echo "Date: "$(date)
      echo "Kernel: "$(uname -a)
      echo "Routing tables:"
      export DEBIAN_FRONTEND=noninteractive
      apt-get -qq update && apt-get -qq -y install net-tools > /dev/null
      route
      echo "Network configuration:"
      ip a
      echo "Firewall:"
      iptables -L
      echo "Updating packages list..."
      apt-get update
      echo "============================================"
      echo "Upgrading packages, non-interactive mode"
      DEBIAN_FRONTEND=noninteractive DEBIAN_PRIORITY=critical apt-get -q -y -o "Dpkg::Options::=--force-confdef" -o "Dpkg::Options::=--force-confold" upgrade
  SHELL
end
