$script = <<-SCRIPT
echo "I like Vagrant"
echo "I love Linux"
date > ~/vagrant_provisioned_at
SCRIPT

# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.boot_timeout = 300
  config.vm.box = "ubuntu/bionic64"
  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end
  #VM 1 ci-server
  config.vm.define "ci-server" do |ciserver|
    ciserver.vm.network "private_network", ip: '192.168.56.60'
    ciserver.vm.hostname = "ci-server"
    #provision with docker
    ciserver.vm.provision :docker
    #provision with docker compose
    ciserver.vm.provision:docker_compose
  end
  #VM 2 server-2
  config.vm.define "server-2" do |server2|
    server2.vm.network "private_network", ip: '192.168.56.61'
    server2.vm.hostname = "server-2"
    #provision with dockery
    server2.vm.provision :docker
    #provision AT20_CONVERT_SERVICE
    server2.vm.provision :file, source: "AT20_CONVERT_SERVICE_TS", destination: "AT20_CONVERT_SERVICE_TS"
    #provision with docker compose
    server2.vm.provision:docker_compose
    server2.vm.provision :file, source: "docker-compose.yaml", destination: "docker-compose.yaml"
    server2.vm.provision :file, source: ".env", destination: ".env"
  end

end
