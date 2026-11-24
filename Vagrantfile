# coding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  config.ssh.insert_key = true

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.linked_clone = true
    vb.memory = "1024"
  end

  # DNS: ns1.olimpo.test (192.168.57.10)
  config.vm.define "dns3" do |dns|
    dns.vm.provider "virtualbox" do |vb|
      vb.name = "dns3"
    end
    dns.vm.hostname = "ns1.olimpo.test"
    dns.vm.network :private_network, ip: "192.168.57.10", hostname: true

    dns.vm.provision "ansible" do |ansible|
      ansible.playbook = "dns.yml"
    end
  end

  # Web: mercurio.olimpo.test (192.168.57.11)
  config.vm.define "web3" do |web|
    web.vm.provider "virtualbox" do |vb|
      vb.name = "web3"
    end
    web.vm.hostname = "mercurio.olimpo.test"
    web.vm.network :private_network, ip: "192.168.57.11", hostname: true

    # Instalación, archivos y sitios virtuales gestionados en web.yml
    web.vm.provision "ansible" do |ansible|
      ansible.playbook = "web.yml"
    end
  end
end
