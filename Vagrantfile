# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "jammy64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/jammy/20220708/jammy-server-cloudimg-amd64-vagrant.box"
  config.ssh.forward_agent = true
  config.ssh.insert_key = false
  config.vm.network :public_network, ip: "192.168.86.233"
  config.vm.provider :virtualbox do |vb|
    host = RbConfig::CONFIG['host_os']
    if host =~ /darwin/
       cpus = `sysctl -n hw.ncpu`.to_i
       mem = `sysctl -n hw.memsize`.to_i / 1024 / 1024 / 4
    elsif host =~ /linux/
       cpus = `nproc`.to_i
       mem = `grep 'MemTotal' /proc/meminfo | sed -e 's/MemTotal://' -e 's/ kB//'`.to_i / 1024 / 2
    else
       cpus = 2
       mem = 2048
    end
    vb.customize ["modifyvm", :id, "--memory", mem]
    vb.customize ["modifyvm", :id, "--cpus", cpus]
    #vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    #vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/vagrant.yml"
    ansible.host_key_checking = false
    ansible.verbose = "vvvv"
  end
end
