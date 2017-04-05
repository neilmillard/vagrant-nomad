# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
# Update apt and get dependencies
sudo yum -y update
sudo yum install -y unzip curl wget vim

# Download Nomad
echo Fetching Nomad...
cd /tmp/
curl -sSL https://releases.hashicorp.com/nomad/0.5.6/nomad_0.5.6_linux_amd64.zip -o nomad.zip

echo Installing Nomad...
unzip nomad.zip
sudo chmod +x nomad
sudo mv nomad /usr/bin/nomad

sudo mkdir -p /etc/nomad.d
sudo chmod a+w /etc/nomad.d

# Set hostname's IP to made advertisement Just Work
sudo sed -i -e "s/.*server.*/$(ip route get 192.168.50 | awk '{print $NF;exit}') $(hostname)/" /etc/hosts
sudo sed -i -e "s/.*client.*/$(ip route get 192.168.50 | awk '{print $NF;exit}') $(hostname)/" /etc/hosts

SCRIPT

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
# Increase memory for VirtualBox
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.box = "centos/7"
  # disable synced folder - https://seven.centos.org/2017/03/updated-centos-vagrant-images-available-v1702-01/
  #config.vm.synced_folder ".", "/vagrant", disabled: true
  # this image uses rsync as default. needs vagrant-vbguest
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
  config.vm.hostname = "nomad"
  config.vm.provision "shell", inline: $script, privileged: false
  config.vm.provision "docker" # just install it

  config.vm.define 'server1' do |manager1|
    manager1.vm.hostname = 'server1'
    manager1.vm.provision 'shell', inline: 'cp /vagrant/cluster/server.hcl /etc/nomad.d/server.hcl'
    manager1.vm.network "private_network", ip: "192.168.50.2"
  end

  config.vm.define 'client1' do |client1|
    client1.vm.hostname = 'client1'
    client1.vm.provision 'shell', inline: 'cp /vagrant/cluster/client.hcl /etc/nomad.d/client.hcl'
    client1.vm.network "private_network", ip: "192.168.50.3"
  end

  config.vm.define 'client2' do |client2|
    client2.vm.hostname = 'client2'
    client2.vm.provision 'shell', inline: 'cp /vagrant/cluster/client.hcl /etc/nomad.d/client.hcl'
    client2.vm.network "private_network", ip: "192.168.50.4"
  end

end
