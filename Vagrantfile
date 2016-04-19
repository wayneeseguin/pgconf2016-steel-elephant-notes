#!/usr/bin/env ruby

VAGRANTFILE_API_VERSION="2"

Mac = %x{printf '00602F%02X%02X%02X' 249 145 115}
Box = ENV["BOX"] ? ENV["BOX"] : "geerlingguy/centos7" # or "freebsd/FreeBSD-11.0-CURRENT"
Network = "10.11.11."
Boxes = 3
ProvisionScript= ENV["PROVISION_SCRIPT"] ? ENV["PROVISION_SCRIPT"] : "./scripts/provision-centos7"
SSHShell = ENV["SSH_SHELL"] ? ENV["SSH_SHELL"] : "bash"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	(0..(Boxes-1)).to_a.each do |index|
		ip = "#{Network}.1#{index}"
		config.vm.define "centos7-pg-#{index}", primary: true do |v|
		  config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true
		  config.vm.box = Box
		  config.vm.base_mac = "#{Mac}"
		  config.ssh.shell = SSHShell
		  config.vm.network "private_network", ip: ip
		  config.vm.provision :shell, inline: "echo '#{ip}' > /tmp/ip"
		  config.vm.provision "file", source: "./scripts/bootstrap-projects", destination: "/tmp/bootstrap-projects"
		  config.vm.provision :shell, :path => ProvisionScript
		end
	end

	config.vm.provider :virtualbox do |v|
		v.customize ["modifyvm", :id, "--memory", "1024"]
		v.customize ["modifyvm", :id, "--cpus", "2"]
		v.customize ["modifyvm", :id, "--hwvirtex", "on"]
		v.customize ["modifyvm", :id, "--audio", "none"]
		v.customize ["modifyvm", :id, "--nictype1", "virtio"]
		v.customize ["modifyvm", :id, "--nictype2", "virtio"]
	end

	config.vm.provider :vmware_fusion do |v|
		v.vmx["memsize"] = "1024"
		v.vmx["numvcpus"] = "1"
	end

  # Timeouts
  config.vm.graceful_halt_timeout = 300 # seconds
  config.vm.boot_timeout = 300 # seconds
end

