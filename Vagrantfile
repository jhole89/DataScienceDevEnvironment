# -*- mode: ruby;-*-
# vi: set ft=ruby:

# Specify Vagrant version, Vagrant API version
Vagrant.require_version ">= 1.6.0"
VAGRANTFILE_API_VERSION = "2"

# Bootstrap script to install host applications
$bootstrap = <<SCRIPT
sudo apt-get -y install wget
sudo apt-get -y install git-all
git config --global user.name "jhole89"
git config --global user.email "joellutman@gmail.com"
cd /vagrant
git clone https://github.com/jhole89/Test_NLP_Project.git
SCRIPT

# Script to workaround multiple quote nesting for Anaconda3 cmd
$jupyterServer = <<SCRIPT
/bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser"
SCRIPT

# Create and configure the VM(s)
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  # Sync /vagrant on host box with OS <project dir>/vagrant
  config.vm.synced_folder ".", "/vagrant"
  
  # Define host box image
  config.vm.box = "ubuntu/trusty64"
  
  # Customise host box settings
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
	vb.customize ["modifyvm", :id, "--cpus", "2"]
  end
  
  # Install applications on the host box
  config.vm.provision "shell", inline: $bootstrap
  
  # Use Docker to pull Anaconda3 and run Jupyter Notebook server
  config.vm.provision "docker" do |d|
    d.pull_images "continuumio/anaconda3"
	d.run "continuumio/anaconda3",
	  args: "-t -p 8888:8888",
	  cmd: $jupyterServer
  end
  
# Forward application ports to localhost
  config.vm.network "forwarded_port", guest: 8888, host: 8888
end
