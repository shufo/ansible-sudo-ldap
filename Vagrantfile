# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define :v do |v|
    v.vm.hostname = "vagrant"
    v.vm.box = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"
    v.vm.network :private_network, ip: "192.168.50.12"
    v.vm.synced_folder ".", "/vagrant"
    v.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", 2048, "--cpus", 2]
      v.gui = false
    end
    v.vm.provision "ansible" do |ansible|
        ansible.sudo = true
        ansible.verbose = "vv"
        ansible.playbook = "site.yml"
        ansible.limit = "all"
    end
  end
end
