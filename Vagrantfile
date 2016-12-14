# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "boxcutter/centos68"

  N = 4

  VAGRANT_VM_PROVIDER = "virtualbox"
  ANSIBLE_RAW_SSH_ARGS = []

  (1..N-1).each do |machine_id|
    ANSIBLE_RAW_SSH_ARGS << "-o IdentityFile=.vagrant/machines/memcache#{machine_id}/#{VAGRANT_VM_PROVIDER}/private_key"
  end

  (1..N).each do |machine_id|
    config.vm.define "memcache#{machine_id}" do |machine|
      machine.vm.hostname = "memcache#{machine_id}"
      machine.vm.network "private_network", ip: "192.168.34.#{10+machine_id}"

      # Only execute once the Ansible provisioner,
      # when all the machines are up and ready.
      if machine_id == N
        machine.vm.provision :ansible do |ansible|
          # Disable default limit to connect to all the machines
          ansible.playbook = 'ansible/playbook.yml'
          ansible.inventory_path = 'ansible/inventories/hosts.ini'
          ansible.limit = 'all'
          ansible.raw_ssh_args = ANSIBLE_RAW_SSH_ARGS
        end
      end
    end
  end
end
