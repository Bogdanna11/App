# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"

  config.vm.network "private_network", ip: "192.168.10.100"


     config.vm.define "controller" do |controller|

      controller.vm.box = "bento/ubuntu-18.04"

      controller.vm.hostname = 'controller'

      controller.vm.network :private_network, ip: "192.168.33.12"

      # config.hostsupdater.aliases = ["development.controller"]

     end
   # creating first VM called web
     config.vm.define "web" do |web|

       web.vm.box = "bento/ubuntu-18.04"
      # downloading ubuntu 18.04 image

       web.vm.hostname = 'web'
       # assigning host name to the VM

       web.vm.network :private_network, ip: "192.168.33.10"
       #   assigning private IP

       #config.hostsupdater.aliases = ["development.web"]
       # creating a link called development.web so we can access web page with this link instread of an IP

     end

   # creating second VM called db
     config.vm.define "db" do |db|

       db.vm.box = "bento/ubuntu-18.04"

       db.vm.hostname = 'db'

       db.vm.network :private_network, ip: "192.168.33.11"

       #config.hostsupdater.aliases = ["development.db"]
     end



end
