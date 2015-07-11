# -*- mode: ruby -*-
# vi: set ft=ruby :

# Requirements:
#
# sudo apt-get install zlib1g-dev python-pip ruby ruby-dev python-dev
# sudo gem install nokogiri
# vagrant plugin install vai
# sudo pip install ansible
#
# For automatic update in /etc/hosts
# vagrant plugin install vagrant-hostsupdater

NAME="podemosencomun"
IP="192.168.33.150"

Vagrant.configure("2") do |config|
  config.vm.define NAME do |machine|
    machine.vm.box     = "neuromobilemarketing/debian-wheezy-debops-amd64"
    machine.vm.guest = :debian
    machine.vm.provider "virtualbox" do |vbox|
      vbox.gui    = false
    end

    machine.vm.hostname = NAME + ".nat.coopit.es"
    machine.vm.network :private_network, ip: IP
    
    machine.vm.synced_folder ".", "/vagrant",  :mount_options => ["dmode=775,fmode=775"], :owner => "vagrant", :group => "vagrant"
  end
  
  config.vm.provision "vai" do |ansible|
    ansible.inventory_dir = "provisioning"
  end
  
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbooks/vagrant.yml"
  end
end