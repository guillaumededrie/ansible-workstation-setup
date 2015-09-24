# -*- mode: ruby -*-
# vi: set ft=ruby :

# set minimal Vagrant version
Vagrant.require_version ">= 1.5.0"

Vagrant.configure("2") do |config|
  config.ssh.forward_agent = true
  # see https://twitter.com/mitchellh/status/525704126647128064
  config.ssh.insert_key = false

  # Multi machine environment
  config.vm.define "my-machine" do |machine|
    machine.vm.hostname = "my-machine.local"
    machine.vm.box = "guillaumededrie/archlinux"
    machine.vm.synced_folder '.', '/vagrant', disabled: true
    machine.vm.network "private_network", ip: "172.16.1.10"

    # Providers specific section
    machine.vm.provider "virtualbox" do |v|
      v.gui = true
      v.cpus = 2
      v.memory = 2048
      v.customize ["modifyvm", :id, "--cpuexecutioncap", 100]
    end
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'playbooks/configuration.yml'

    ansible.extra_vars = {
      ansible_python_interpreter: "/usr/bin/python2"
    }
    #ansible.tags = ['']
    #ansible.skip_tags = ['']
    #ansible.verbose = 'vvvv'
    #ansible.raw_arguments = ['--check','--diff']
  end
end
