# -*- mode: ruby -*-
# vi: set ft=ruby :
#
#Define the list of machines
cluster = {
	:controller => {
		:hostname => "controller",
		:ipaddress => "192.168.56.200",
		:image => "ubuntu/jammy64"
	},
	:node1 => {
		:hostname => "node1",
		:ipaddress => "192.168.56.201",
		:image => "ubuntu/jammy64",
        :cpus => "1"
	},
	:node2 => {
		:hostname => "node2",
		:ipaddress => "192.168.56.202",
		:image => "rockylinux/9",
        :cpus => "2"
	}
}

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |global|
	cluster.each_pair do |name,options|
		global.vm.define name do |node|
			#per VM customizations
			node.vm.box = options[:image]
			node.vm.hostname = "#{name}"
			node.vm.network :private_network, ip: options[:ipaddress]
			node.vm.provider :virtualbox do |v|
				v.cpus = options[:cpus] || 1
			end
            node.vm.provision :ansible do |checks|
                checks.playbook = "provisioning/checks.yml"
            end
		end
	end
end