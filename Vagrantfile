# -*- mode: ruby -*-
# vi: set ft=ruby :

# Specify Vagrant version, Vagrant API version
Vagrant.require_version ">= 1.6.0"
VAGRANTFILE_API_VERSION = "2"

$configureHost = <<SCRIPT
sudo apt-get -y install git-all
sudo apt-get -y install wget
SCRIPT

# Script to workaround multiple quote nesting
$jupyterServer = <<SCRIPT
/bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser"
SCRIPT

# Create and configure the VM(s)
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  # Define host box image
  config.vm.box = "ubuntu/trusty64"
  
  # Customise host box settings
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
	vb.customize ["modifyvm", :id, "--cpus", "2"]
  end
  
  # Install applications on the host box
  config.vm.provision "shell", inline: $configureHost
  
  # Use Docker provisioner to pull Anaconda3 and run Jupyter Notebook server on port 8888
  config.vm.provision "docker" do |d|
    d.pull_images "continuumio/anaconda3"
	d.run "continuumio/anaconda3",
	  args: "-t -p 8888:8888",
	  cmd: $jupyterServer
  end
  
  # Forward 8888 to localhost:8888
  config.vm.network "forwarded_port", guest: 8888, host: 8888
  config.vm.synced_folder ".", "/vagrant"
end
