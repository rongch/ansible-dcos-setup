# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  #config.vm.box = "ubuntu/trusty64"
  config.vm.box = "bento/centos-7.2"
  #config.vm.box = "puphpet/centos65-x64"
  config.vm.synced_folder ".", "/vagrant"
  #config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=700,fmode=600"]
  #config.vm.provider "virtualbox" do |v|
  #  #v.memory = 2048
  #  v.memory = 1024
  #end

  #config.vm.provision :shell, path: "bootstrap.sh"
  #config.vm.provision :shell, path: "bootstrap_centos.sh"

  config.vm.define "bootstrap" do |node|
    node.vm.hostname = "bootstrap"
    node.vm.provider 'virtualbox' do |v|
      v.name = node.vm.hostname
      v.cpus = 2
      v.memory = 1024
    end
    #node.vm.provision :shell, path: "bootstrap_ansible.sh" # for Ubuntu
    #node.vm.provision :shell, path: "ansible_install.sh"  # for all
    #node.vm.provision "file", source: "./ansible.cfg", destination: "/home/vagrant/.ansible.cfg"
    node.vm.network "private_network", ip: "192.168.144.120"
    #node.vm.network "forwarded_port", guest: 2376, host: 2376
    #node.vm.network "forwarded_port", guest: 2375, host: 2375
  end
  #config.vm.define "nexus3" do |node|
  #  node.vm.hostname = "nexus3"
  #  node.vm.network "private_network", ip: "10.100.199.250"
  #end

  (0..0).each do |i|
    config.vm.define "mesos-master-#{i}" do |node|
      node.vm.hostname = "mesos-master-#{i}"
      node.vm.provider 'virtualbox' do |v|
        v.name = node.vm.hostname
        v.cpus = 2
        v.memory = 1024
      end
      node.vm.network "private_network", ip: "192.168.144.13#{i}"
    end
  end
  config.vm.define "mesos-agent-00" do |node|
    node.vm.hostname = "mesos-agent-00"
    node.vm.provider 'virtualbox' do |v|
      v.name = node.vm.hostname
      v.cpus = 4
      #v.memory = 2048
      v.memory = 4096
    end
    node.vm.network "private_network", ip: "192.168.144.140"
  end
  (1..2).each do |i|
    config.vm.define "mesos-agent-0#{i}" do |node|
      node.vm.hostname = "mesos-agent-0#{i}"
      node.vm.provider 'virtualbox' do |v|
        v.name = node.vm.hostname
        v.cpus = 4
        #v.memory = 2048
        v.memory = 1024
      end
      node.vm.network "private_network", ip: "192.168.144.14#{i}"
    end
  end
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
end
