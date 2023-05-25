# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.box_check_update = true

  
  config.vm.provider "virtualbox" do |v|
    v.name = "postgres"
    v.memory = 2048
    v.cpus = 2
  end

  config.vm.network "forwarded_port", guest: 5432, host: 5432

  config.vm.provision "shell", inline: <<-SHELL
    echo 'Download Postgres'
    sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
    sudo apt update
    sudo apt install -y --download-only postgresql-8.4
    sudo apt install -y postgresql-common
    sudo service postgresql start
  SHELL
end
