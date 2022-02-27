# -*- mode: ruby -*-
# vi: set ft=ruby :

IMAGE_NAME = "ubuntu/focal64"
N = 2

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
  end
    
  config.vm.define "master" do |master|
    master.vm.box = IMAGE_NAME
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.33.10"
    master.vm.provision "ansible" do |ansible|
      ansible.playbook = "./playbook.yml"
      ansible.extra_vars = {
        node_ip: "192.168.33.10",
      }
    end
  end

  (1..N).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.box = IMAGE_NAME
      node.vm.hostname = "node#{i}"
      node.vm.network "private_network", ip: "192.168.33.#{i + 10}"
      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "./playbook.yml"
        ansible.extra_vars = {
          node_ip: "192.168.33.#{i + 10}",
        }
      end
    end
  end
end