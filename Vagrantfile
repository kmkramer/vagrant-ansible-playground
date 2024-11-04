Vagrant.configure("2") do |machine|
    
    machine.vm.box = "ubuntu/jammy64"

    machine.vm.define "node1" do |config|
        config.vm.hostname = "node1"
		config.vm.network :private_network, ip: "192.168.56.201"
	end

    machine.vm.define "node2" do |config|
        config.vm.hostname = "node2"
        config.vm.box = "rockylinux/9"
		config.vm.network :private_network, ip: "192.168.56.202"
        config.vm.provider :virtualbox do |v|
		    v.cpus = 2
		end
    end

    machine.vm.define "controller" do |config|
        config.vm.hostname = "controller"
        config.vm.network :private_network, ip: "192.168.56.200"
        
        config.vm.provision :ansible_local do |ansible|
                ansible.verbose         = true
                ansible.install         = true
                ansible.limit           = "all"
                ansible.config_file     = "/vagrant/ansible/ansible.cfg"
                ansible.inventory_path  = "/vagrant/ansible/inventory.ini"
                ansible.playbook        = "/vagrant/ansible/checks.yml"
        end
	end
end