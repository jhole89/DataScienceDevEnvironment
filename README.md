# Data Science Development Environment
A deployable data science environment built to run on any OS that supports Vagrant.
This makes use of Vagrant to deploy a lightweight virtualbox image which installs docker and runs an Anaconda container.
The reasoniny behind this is that there are known issues with trying to run Docker on Windows so it made more sense to run it on a Linux box.

![Deployable Data Science](https://www.continuum.io/sites/default/files/anaconda_docker_2_0.png)


## Prerequisites
1. [VirtualBox ](https://www.virtualbox.org/wiki/Downloads)
2. [Vagrant](https://www.vagrantup.com/downloads.html)


## Usage
Once you have installed VirtualBox and Vagrant simply navigate to the Vagrantfile and run `vagrant up` from the command line.
Jupyter Notebooks can then be accessed from localhost:8888.