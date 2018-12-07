# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

ipprefix = "192.168.33"

nodes = [
  { :name => "master", :ip => 11, :script => "init-master" },
  { :name => "slave1", :ip => 12, :script => "init-slave" },
  { :name => "slave2", :ip => 13, :script => "init-slave" },
]

open("vm-hosts", "w") do |hosts|
  nodes.each do |item|
    hosts.print("#{ipprefix}.#{item[:ip]} #{item[:name]}\n")
  end
end

Vagrant.configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:name] do |n|
      n.vm.box = "ubuntu/bionic64"
      n.vm.box_check_update = false
      n.vm.network "private_network", ip: "#{ipprefix}.#{node[:ip]}"
      n.vm.hostname = node[:name]
      n.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
        vb.cpus = 2
      end
      n.vm.provision "shell", path: node[:script]
    end
  end
end
