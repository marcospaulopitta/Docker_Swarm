Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"

  config.vm.define "master" do |master|
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "100"
    master.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 2
    end
    master.vm.provision "shell", inline: <<-SHELL
      # Instalação do Docker
      apt-get update
      apt-get install -y apt-transport-https ca-certificates curl software-properties-common
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
      echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      apt-get update
      apt-get install -y docker-ce docker-ce-cli containerd.io
      usermod -aG docker vagrant

      # Configuração do Swarm
      docker swarm init --advertise-addr 192.168.1.100
    SHELL
  end

  config.vm.define "node01" do |node01|
    node01.vm.hostname = "node01"
    node01.vm.network "private_network", ip: "101"
    node01.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 2
    end
    node01.vm.provision "shell", inline: <<-SHELL
      # Instalação do Docker
      apt-get update
      apt-get install -y apt-transport-https ca-certificates curl software-properties-common
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
      echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      apt-get update
      apt-get install -y docker-ce docker-ce-cli containerd.io
      usermod -aG docker vagrant

      # Adição ao cluster Swarm
      docker swarm join --token <token> 192.168.1.100:2377
    SHELL
  end

  config.vm.define "node02" do |node02|
    node02.vm.hostname = "node02"
    node02.vm.network "private_network", ip: "102"
    node02.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 2
    end
    node02.vm.provision "shell", inline: <<-SHELL
      # Instalação do Docker
      apt-get update
      apt-get install -y apt-transport-https ca-certificates curl software-properties-common
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
      echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      apt-get update
      apt-get install -y docker-ce docker-ce-cli containerd.io
      usermod -aG docker vagrant

      # Adição ao cluster Swarm
      docker swarm join --token <token> 192.168.1.100:2377
    SHELL
  end
  end