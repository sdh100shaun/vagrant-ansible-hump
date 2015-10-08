##################################################
# Generated by phansible.com
##################################################

#If your Vagrant version is lower than 1.5, you can still use this provisioning
#by commenting or removing the line below and providing the config.vm.box_url parameter,
#if it's not already defined in this Vagrantfile. Keep in mind that you won't be able
#to use the Vagrant Cloud and other newer Vagrant features.
Vagrant.require_version ">= 1.5"

Vagrant.configure("2") do |config|

    config.vm.provider :virtualbox do |v|
        v.name = "hump"
        v.customize [
            "modifyvm", :id,
            "--name", "hump",
            "--memory", 512,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end

     config.vm.box = 'chef/centos-7.1'
  
    
    config.vm.network :private_network, ip: "192.168.20.30"
    config.ssh.forward_agent = true

    #############################################################
    # Ansible provisioning (you need to have ansible installed)
    #############################################################

    
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.inventory_path = "ansible/inventories/dev"
        ansible.limit = 'all'
        ansible.extra_vars = {
            private_interface: "192.168.20.30",
            hostname: "hump"
        }
    end
    
    config.vm.synced_folder "./", "/srv/", type: "nfs"
end
