# -*- mode: ruby -*-
# vi: set ft=ruby :

NUM_WORKER_NODES=2
IP_NW="10.0.0."
IP_START=10
Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"

  (1..NUM_WORKER_NODES).each do |i|
    config.vm.define "worker#{i}" do |node|
      node.vm.hostname = "worker#{i}"
      node.vm.network "private_network", ip: IP_NW + "#{IP_START + i}"
      node.vm.provider "virtualbox" do |vb|
          vb.memory = 2048
          vb.cpus = 2
          vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      end
      node.vm.provider "hyperv" do |hv|
        hv.cpus = 2
        hv.memory = 2048
        hv.vm_integration_services = {
          guest_service_interface: true,
          CustomVMSRV: true
        }
      end
      node.vm.provider "vmware_desktop" do |v|
        v.vmx["memsize"] = "2048"
        v.vmx["numvcpus"] = "2"
      end
    end
  end

  config.vm.define "master" , primary: true do |master|
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: IP_NW + "#{IP_START}"
    master.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
    master.vm.provider "hyperv" do |hv|
      hv.cpus = 2
      hv.memory = 4096
      hv.maxmemory = 4096
      hv.vm_integration_services = {
        guest_service_interface: true,
        CustomVMSRV: true
      }
    end
    master.vm.provider "vmware_desktop" do |v|
      v.vmx["memsize"] = "4096"
      v.vmx["numvcpus"] = "2"
    end
    master.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.groups = {
        "master" => ["master"],
        "node" => ["worker[1:#{NUM_WORKER_NODES}]"]
      }
      ansible.limit = "all"
      ansible.become = true
      ansible.verbose = "-v"
      ansible.extra_vars = {
        switch_mirror: true
      }
    end
  end

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

end
