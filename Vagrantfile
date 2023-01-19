Vagrant.require_version ">= 2.2.0"
require 'yaml'
conf=YAML.load_file("config.yaml")
Vagrant.configure("2") do |config|
    config.ssh.private_key_path = conf['ssh_private_key_path']
    config.vbguest.auto_update = true
    config.vm.define conf['vm_name'] do |box|
        box.vm.box = conf['base_box']
        box.vm.network "private_network", ip: conf['ip']
        box.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--memory", conf['memory']]
            vb.customize ["modifyvm", :id, "--cpus", conf['cpus']]
        end
        box.vm.provision 'ansible' do |ansible|
            ansible.compatibility_mode = "2.0"
            ansible.verbose = "v"
            ansible.tags = 'all'
            ansible.skip_tags = ''
            ansible.playbook = "./playbook.yml"
        end
    end
end
