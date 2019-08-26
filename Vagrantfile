# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.disksize.size = '50GB'

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  #config.vm.network "private_network", ip: "192.168.56.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  #config.vm.network "public_network"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
    vb.memory = "8192"
    vb.cpus = 6
    vb.customize ["modifyvm", :id, "--pae", "on"]
  end

  # Enable provisioning with Ansible - install base requirements
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provisioning/base/playbook.yml"
  end

  config.vm.provision :reload

  # Enable provisioning with Ansible - configure Kubernetes
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provisioning/kubernetes/playbook.yml"
  end
end
