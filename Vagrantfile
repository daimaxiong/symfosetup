Vagrant.require_version ">= 2.2.0"
require 'yaml'

Vagrant.configure("2") do |config|
    config.vbguest.auto_update = false

    config.vm.define "symfo" do |box|
        box.vm.box = 'vb-fedora-35'
        box.vm.network "private_network", ip: "192.168.35.10"
        box.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--memory", 2048]
            vb.customize ["modifyvm", :id, "--cpus", 2]
        end
        box.vm.synced_folder "../src/", "/var/www/test", create: true, owner: "apache", group: "apache", mount_options: ["dmode=775,fmode=775"]
        box.vm.provision :ansible do |ansible|
            ansible.compatibility_mode = "2.0"
            ansible.verbose = "v"
            ansible.tags = 'all'
            ansible.skip_tags = ''
            ansible.playbook = "playbook.yml"
        end
    end
end
