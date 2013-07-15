# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

#  config.vm.box = "ubuntu-13.04"

    # General virtualbox settings
    config.vm.provider :virtualbox do |vb|
        vb.gui = true
    end

    # Foreman VM
    config.vm.define :foreman do |vm_config|

        vm_config.vm.hostname   = "foreman.cloud.gwdg.de"
        vm_config.vm.box        = "ubuntu-13.04"

        vm_config.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", 1536]
        end

        # Provisioning network
        vm_config.vm.network :private_network, ip: "10.1.255.2",    netmask: "255.255.0.0"

        vm_config.vm.network :forwarded_port, guest: 80, host: 8080
        vm_config.vm.network :forwarded_port, guest: 443, host: 8443

    end

end
