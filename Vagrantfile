# -*- mode: ruby -*-
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.box_check_update = false
  config.vm.network "forwarded_port", guest: 9000, host: 9000
  config.vm.network "public_network", use_dhcp_assigned_default_route: true
  config.vm.hostname = "sentry"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
    vb.cpus = "2"
  end

   config.vm.provision "shell", inline: <<-SHELL
     sudo apt update
     sudo apt upgrade -y
     sudo apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
     sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
     sudo apt-key fingerprint 0EBFCD88
     sudo add-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
     sudo apt update
     sudo apt install -y docker-ce docker-ce-cli containerd.io
     sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
     sudo chmod +x /usr/local/bin/docker-compose
     git clone https://github.com/getsentry/onpremise.git
     cd onpremise/
     sudo ./install.sh
     docker-compose up -d
   SHELL
end
