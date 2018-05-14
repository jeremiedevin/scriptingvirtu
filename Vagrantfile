# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url = "https://vagrantcloud.com/ubuntu/trusty64"
  
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 1024, "--cpus", 1]
  end
  
  config.vm.define :haproxy, primary: true do |haproxy_config|
   haproxy_config.vm.hostname = 'haproxy'
   haproxy_config.vm.synced_folder ".", "/vagrant", disabled: true
   haproxy_config.vm.network :forwarded_port, guest: 8080, host: 8080
   haproxy_config.vm.network :forwarded_port, guest: 80, host: 8081
   haproxy_config.vm.network :private_network, ip: "172.28.33.10"
   haproxy_config.vm.provision :shell, :path => "haproxy-setup.sh"
  end

  config.vm.define :web1, second: true do |web1_config|
    web1_config.vm.hostname = 'web1'
	web1_config.vm.synced_folder ".", "/vagrant", disabled: true
    web1_config.vm.synced_folder "/Documents/CoursScriptingVirtu/data/web1", "/var/www/html"
    web1_config.vm.network :private_network, ip: "172.28.33.11", netmask: "255.255.255.0"
    web1_config.vm.provision :shell, :path => "web-setup.sh"
  end

  config.vm.define :web2, third: true do |web2_config|
    #Nom de la VM
    web2_config.vm.hostname = 'web2'
	web2_config.vm.synced_folder ".", "/vagrant", disabled: true
    web2_config.vm.synced_folder "/Documents/CoursScriptingVirtu/data/web2", "/var/www/html"
    web2_config.vm.network :private_network, ip: "172.28.33.12", netmask: "255.255.255.0"
    web2_config.vm.provision :shell, :path => "web-setup.sh"
  end
end


# Pages web : http://127.0.0.1:8081/
# Connexion interface HaProxy : http://127.0.0.1:8080/haproxy?stats/