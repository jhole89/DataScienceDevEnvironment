# -*- mode: ruby;-*-
# vi: set ft=ruby:

# Specify Vagrant version, Vagrant API version
Vagrant.require_version ">= 1.6.0"
VAGRANTFILE_API_VERSION = "2"

# Create and configure the VM(s)
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  # Sync /vagrant on host box with OS <project dir>/vagrant
  config.vm.synced_folder ".", "/vagrant"
  
  # Define host box image
  config.vm.box = "ubuntu/xenial64"
  
  # Customise host box settings
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
	vb.customize ["modifyvm", :id, "--cpus", "2"]
  end
  
  # Run Ansible from the Vagrant VM
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provisioning/main.yml"
  end
  
# Forward application ports to localhost
  config.vm.network "forwarded_port", guest: 8888, host: 8888
end
