# -*- mode: ruby -*-
# vi: set ft=ruby :

#-----------------------------------------------------------------------------------------------------------------#
# 
# @Autor : keeprich
# Description : Vagrant file and script for provisionning Jenkins installation for Utrains DevOps Courses
# Date : 03/22/2022
#   
#------------------------------------------------------------------------------------------------------------------#

Vagrant.configure("2") do |config|
    # jenkinshost-utrains : is the name that have our server
    config.vm.define "jenkins" do |jenkinshost|
      jenkinshost.vm.box = "centos/7"
      jenkinshost.vm.hostname = "jenkins"
      jenkinshost.vm.network "private_network", ip: "192.168.56.170"
      #jenkinshost.vm.box_url = "utrains/centos7"
      jenkinshost.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--memory", 2048]
        v.customize ["modifyvm", :id, "--name", "jenkins"]
        v.customize ["modifyvm", :id, "--cpus", "2"]
      end
      config.vm.provision "shell", inline: <<-SHELL
        sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config   
        sudo systemctl restart sshd
      SHELL
      #install_jenkinshost.sh : This is the script that will take care of the installation of Java, Jenkins server and some utilities
      jenkinshost.vm.provision "shell", path: "install-jenkins.sh"
    end
  end
