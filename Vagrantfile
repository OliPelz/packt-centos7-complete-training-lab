# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

lab_machines = {
  "master"  => { :ip => "192.168.1.100", :cpus => 1, :mem => 1024 },
  "client1" => { :ip => "192.168.1.101", :cpus => 1, :mem => 1024 },
  "client2" => { :ip => "192.168.1.102", :cpus => 1, :mem => 1024 },
  "slave"   => { :ip => "192.168.1.103", :cpus => 1, :mem => 1024 },
  "repo"    => { :ip => "192.168.1.104", :cpus => 1, :mem => 1024 }
}

Vagrant.configure("2") do |config|

# like global settings valid for all machines
   config.vm.provider "virtualbox"
   config.vm.box = "centos/7"
   config.ssh.insert_key = false

   lab_machines.each_with_index do |(hostname, infos), index|
    config.vm.define "#{hostname}" do |machine|
      machine.vm.network "private_network", ip: "#{infos[:ip]}"
      if index == lab_machines.size - 1
   	 machine.vm.provision :ansible do |ansible|
	   ansible.limit = "all"
           ansible.playbook = "playbook.yml"
	   ansible.inventory_path = "inventory"
	 end
      end
    end
   end
end
