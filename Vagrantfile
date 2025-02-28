# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    # Kubernetes Master Server
    config.vm.define "rk8s" do |rk8s|
      rk8s.vm.box = "bento/ubuntu-24.04"
      rk8s.vm.hostname = "rk8s.example.com"
      rk8s.vm.network "private_network", ip: "192.168.56.110"
      rk8s.vm.provider "virtualbox" do |v|
        v.name = "rk8s"
        v.memory = 16384
        v.cpus = 4
        v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/code", "1"]
      end
      # setup VM options
      rk8s.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant", disabled: false
      rk8s.vm.provision "shell", inline: "echo 192.168.56.110 rk8s.example.com >> /etc/hosts"
      # update software and install requirements
      rk8s.vm.provision "shell", inline: "apt-get update && apt-get upgrade -y"
      rk8s.vm.provision "shell", inline: <<-SHELL
apt-get install -y build-essential ca-certificates curl gnupg lsb-release binfmt-support \
git libsystemd-dev systemd-container golang && \
mkdir -p /etc/apt/keyrings && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --batch --dearmor -o /etc/apt/keyrings/docker.gpg && \
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu  \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && \
apt-get update && apt-get install -y docker-ce docker-ce-cli containerd.io \
docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
SHELL
      # setup our environment for building docker images
      rk8s.vm.provision "shell", inline: "usermod -aG docker vagrant"
      rk8s.vm.provision "shell", inline: "newgrp docker"
    end
end