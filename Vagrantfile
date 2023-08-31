Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "servidor-web"
  config.vm.box_download_insecure=true

  # Configurações de Rede
  

  # Interface de rede privada com IP estático

  config.vm.network "private_network", type: "static", ip: "192.168.7.80"
  config.vm.network "private_network", type: "static", ip: "192.168.0.80"
  #config.vm.network "public_network", type: "dhcp"



  # Porta 80 da máquina virtual para a porta 8080 da máquina local

  config.vm.network "forwarded_port", guest: 80, host: 8080  

  # Configurações do Provedor

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 1
  end

  # Configurações do Diretorio Compartilhado

  config.vm.synced_folder "./shared_vagrant", "/shared_linux"  

  # Configurações de Shell

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y apache2
    apt-get install -y htop
    apt-get install nano
    apt-get install python3
    ufw allow 8080/tcp
    systemctl start apache2
    systemctl enable apache2

  SHELL

end