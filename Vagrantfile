# -*- mode: ruby -*-
# vim: set ft=ruby ts=2 sw=2 expandtab:

# Install required plugins
required_plugins = %w( vagrant-vbguest )
required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure(2) do |config|
  # Disables vbguest auto update
  config.vbguest.auto_update = false

  ENV['VAGRANT_DEFAULT_PROVIDER'] = 'virtualbox'

  # All machines will be based on CentOS 6.8
  config.vm.box = "boxcutter/centos68"

  # JBoss EAP Domain Controller (master/primary)
  config.vm.define "master1" do |master1|
    master1.vm.hostname="master1"
    master1.vm.network "private_network", ip: "172.17.6.81"
    master1.vm.provision "shell", path: ".scripts/instalar-master", privileged: false
  end

  # JBoss EAP Domain Controller (master/backup)
  config.vm.define "master2" do |master2|
    master2.vm.hostname="master2"
    master2.vm.network "private_network", ip: "172.17.6.82"
    master2.vm.provision "shell", path: ".scritps/instalar-master", privileged: false
  end

  # JBoss EAP Host Controller (slave1)
  config.vm.define "slave1" do |slave1|
    slave1.vm.hostname="slave1"
    slave1.vm.network "private_network", ip: "172.17.6.83"
    slave1.vm.provision "shell", path: ".scripts/instalar-slave", privileged: false
    slave1.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
  end

  # JBoss EAP Host Controller (slave2)
  config.vm.define "slave2" do |slave2|
    slave2.vm.hostname="slave2"
    slave2.vm.network "private_network", ip: "172.17.6.84"
    slave2.vm.provision "shell", path: ".scripts/instalar-slave", privileged: false
    slave2.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
  end
end
