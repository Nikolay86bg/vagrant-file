# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Box Settings
  config.vm.box = "ubuntu/xenial64"

  # Provider Settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end

  # Network Settings
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "private_network", ip: "192.168.42.120"
  # config.vm.network "public_network"

  # Folder Settings
  config.vm.synced_folder "../source/", "/var/www/html/", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

  # Provision Settings
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y git

    apt-get install apache2 -y
    systemctl start apache2.service

    a2enmod proxy proxy_http
    a2enmod proxy proxy_fcgi

    apt-add-repository ppa:ondrej/php
    apt update
    apt-cache pkgnames | grep php7.2
    apt-get install php -y
    apt-get install php-{bcmath,bz2,intl,gd,mbstring,mysql,zip,fpm,xml} -y
    systemctl restart apache2.service


    service apache2 restart
  SHELL
end
