# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "debian/stretch64"
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
    v.name = "devpl"
    v.memory = 1024
    v.cpus = 2
    # v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    # v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Default folder sharing
  config.vm.synced_folder ".", "/vagrant", id: "vagrant-root",
  owner: "root",
  group: "sudo",
  mount_options: ["dmode=775,fmode=774"]

  config.vm.hostname = "devpl.uk"
  config.vm.network :private_network, ip: "192.168.33.34"

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :devpl do |devpl|
  end

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "provisioning/main.yml"
    ansible.inventory_path = "provisioning/inventory"
    ansible.become = true
  end

end
