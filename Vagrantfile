# -*- mode: ruby -*-
# vim: set ft=ruby ts=2 sw=2 expandtab:

# Instala Plugins ...
required_plugins = %w( vagrant-vbguest )
required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure(2) do |config|
  # Desabilita o auto update do vbguest
  config.vbguest.auto_update = false

  # Ajusta do default provider para ser o Virtualbox
  ENV['VAGRANT_DEFAULT_PROVIDER'] = 'virtualbox'

  # Todas as VMs são baseadas no CentOS 6.8
  config.vm.box = "boxcutter/centos68"

  # JBoss EAP Domain Controller (master) primário
  config.vm.define "master1" do |master1|
    master1.vm.hostname="master1"
    master1.vm.network "private_network", ip: "172.17.6.81"
    master1.vm.provision "shell", path: "master1/instalar", privileged: false
  end

  # JBoss EAP Domain Controller (master) backup
  config.vm.define "master2" do |master2|
    master2.vm.hostname="master2"
    master2.vm.network "private_network", ip: "172.17.6.82"
    master2.vm.provision "shell", path: "master2/instalar", privileged: false
  end

  # JBoss EAP Host Controller (slave) slave1
  config.vm.define "slave1" do |slave1|
    slave1.vm.hostname="slave1"
    slave1.vm.network "private_network", ip: "172.17.6.83"
    slave1.vm.provision "shell", path: "slave1/instalar", privileged: false
    slave1.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
  end

  # JBoss EAP Host Controller (slave) slave2
  config.vm.define "slave2" do |slave2|
    slave2.vm.hostname="slave2"
    slave2.vm.network "private_network", ip: "172.17.6.84"
    slave2.vm.provision "shell", path: "slave2/instalar", privileged: false
    slave2.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
  end
end
