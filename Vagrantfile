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
        vm_config.vm.box        = "ubuntu-12.04.2"

        vm_config.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", 1536]
        end

        # Management network
        vm_config.vm.network :private_network, ip: "10.1.1.2",      netmask: "255.255.255.0"

        # Provisioning network
        vm_config.vm.network :private_network, ip: "10.1.254.254",  netmask: "255.255.255.0"

        vm_config.vm.network :forwarded_port, guest: 80, host: 8080
        vm_config.vm.network :forwarded_port, guest: 443, host: 8443

    end

    # Define blank vm for provisioning
    config.vm.define :blank1 do |vm_config|

        vm_config.vm.box        = "blank-amd64"

        vm_config.vm.provider :virtualbox do |vb|

            vb.customize ["modifyvm", :id, "--memory", 512]

            # generate a new mac address for each node, to make them unique
#            vb.customize ["modifyvm", :id, "--macaddress1", "auto"]
            vb.customize ["modifyvm", :id, "--macaddress1", "123456789012"]

            # put primary network interface into hostonly network segement
            vb.customize ["modifyvm", :id, "--nic1", "hostonly"]
            vb.customize ["modifyvm", :id, "--hostonlyadapter1", "vboxnet2"]

            # pxe boot the node
            vb.customize ["modifyvm", :id, "--boot1", "net"]

        end

    end

end
