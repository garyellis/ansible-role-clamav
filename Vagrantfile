# -*- mode: ruby -*-
# vi: set ft=ruby ts=2 sw=2 tw=0 et :
require 'yaml'


boxes = YAML.load_file('boxes.yml')

def create_box(hostname, cpus, memory, ip_address, box, shell_script_path=nil, shell_env=nil, ansible_playbook=nil)
  Vagrant.configure(2) do |config|
    # vagrant-hostmanager plugin
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.ignore_private_ip = false
    config.hostmanager.include_offline = true

    config.vm.define hostname do |vm_config|
      vm_config.vm.provider :virtualbox do |v|
        v.name = hostname
        v.memory = memory
        v.cpus = cpus
      end

      vm_config.vm.box = box
      vm_config.vm.hostname = hostname
      vm_config.vm.network :private_network, ip: ip_address

      unless shell_script_path.nil?
        vm_config.vm.provision :shell do |shell|
          shell.path = shell_script_path
          shell.env = shell_env
        end
      end

      unless ansible_playbook.nil?
        vm_config.vm.provision :ansible do |ansible|
          ansible.playbook = ansible_playbook
          ansible.raw_arguments = ['--become']
      end

      end

    end

  end

end


boxes['boxes'].each do |box|
  create_box(box['hostname'],
             box['cpus'],
             box['memory'],
             box['ip'],
             box['box'],
             box['shell_script_path'],
             box['shell_env'],
             box['ansible_playbook'])

end
