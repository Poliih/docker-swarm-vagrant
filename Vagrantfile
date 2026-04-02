Vagrant.configure("2") do |config|

  BOX_IMAGE = "ubuntu/focal64"

  # Script para instalar Docker
  DOCKER_SCRIPT = <<-SHELL
    apt-get update
    apt-get install -y docker.io
    systemctl start docker
    systemctl enable docker
    usermod -aG docker vagrant
  SHELL

  # MASTER
  config.vm.define "master" do |master|
    master.vm.box = BOX_IMAGE
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.56.10"
    master.vm.provision "shell", inline: DOCKER_SCRIPT

    master.vm.provision "shell", inline: <<-SHELL
      docker swarm init --advertise-addr 192.168.56.10
      docker swarm join-token worker -q > /vagrant/token.txt
    SHELL
  end

  # NODE 01
  config.vm.define "node01" do |node|
    node.vm.box = BOX_IMAGE
    node.vm.hostname = "node01"
    node.vm.network "private_network", ip: "192.168.56.11"
    node.vm.provision "shell", inline: DOCKER_SCRIPT

    node.vm.provision "shell", inline: <<-SHELL
      while [ ! -f /vagrant/token.txt ]; do sleep 2; done
      docker swarm join --token $(cat /vagrant/token.txt) 192.168.56.10:2377
    SHELL
  end

  # NODE 02
  config.vm.define "node02" do |node|
    node.vm.box = BOX_IMAGE
    node.vm.hostname = "node02"
    node.vm.network "private_network", ip: "192.168.56.12"
    node.vm.provision "shell", inline: DOCKER_SCRIPT

    node.vm.provision "shell", inline: <<-SHELL
      while [ ! -f /vagrant/token.txt ]; do sleep 2; done
      docker swarm join --token $(cat /vagrant/token.txt) 192.168.56.10:2377
    SHELL
  end

  # NODE 03
  config.vm.define "node03" do |node|
    node.vm.box = BOX_IMAGE
    node.vm.hostname = "node03"
    node.vm.network "private_network", ip: "192.168.56.13"
    node.vm.provision "shell", inline: DOCKER_SCRIPT

    node.vm.provision "shell", inline: <<-SHELL
      while [ ! -f /vagrant/token.txt ]; do sleep 2; done
      docker swarm join --token $(cat /vagrant/token.txt) 192.168.56.10:2377
    SHELL
  end

end