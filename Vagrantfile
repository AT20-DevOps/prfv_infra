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

  config.vm.box = "ubuntu/bionic64"
  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end
    #configure provisioners on tha machine
  config.vm.provision :docker
  #copiar shell hacer correr
  config.vm.provision :shell, path: "bootstrapup.sh"
  config.vm.provision :file, source: "newfile", destination: "newfile"
  #copiar archivos o carpetas
  config.vm.provision :file, source: "HTML", destination: "HTMLDIR"
  config.vm.define "server-1" do |dockerserver|
    dockerserver.vm.network "private_network", ip: '192.168.56.60'
    dockerserver.vm.hostname = "dockerserver"
    #si se quiere ahcer correr algo solo en el server

    dockerserver.vm.provision :shell, inline: "echo hi class from shell inline"
    dockerserver.vm.provision :shell, inline: $script
    dockerserver.vm.provision "shell" do |s|
      s.inline = "echo $1"
      s.args = ["AT", "Class!"]
    end
    dockerserver.vm.provision "docker" do |d|
      d.run "hello-world"
    end
  end

end
