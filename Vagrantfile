# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  ##############
  # VPP VM A~F #
  ##############
  (2001..2006).each do |host_id|
    vm_name  = "SRv6-" + host_id.to_s
    config.vm.define vm_name do |srv6|
      srv6.vm.hostname = "SRv6-#{host_id}"
      srv6.vm.box = "ubuntu/bionic64"
      srv6.vm.network "forwarded_port", guest: 22, host: host_id.to_i, host_ip: "127.0.0.1"

      case host_id
      when 2001 then 
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db1::1",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2001"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db2::1",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2002"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db3::1",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2003"

      when 2002 then
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db2::2",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2002"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db4::1",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2004"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db5::1",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2005"

      when 2003 then
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip:"2001:db3::2",
          netmask:"64",
          virtualbox__intnet: "srv6_seg2003"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db4::2",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2004"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db6::1",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2006"
      
      when 2004 then
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db5::2",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2005"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db7::1",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2007"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db8::1",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2008"

      when 2005 then
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip:"2001:db6::2",
          netmask:"64",
          virtualbox__intnet: "srv6_seg2006"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db7::2",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2007"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db9::1",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2008"

      when 2006 then
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db8::2",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2008"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db9::2",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2009"
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db10::1",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2010"
      end

      srv6.vm.provider "virtualbox" do |vb|
        # Customize the amount of memory on the VM:
        vb.memory = "1024"
      end

      srv6.vm.provision "shell", inline: <<-SHELL
#        curl -s https://packagecloud.io/install/repositories/fdio/1904/script.deb.sh | sudo bash
#        apt update
#        apt install vpp -y
#        apt install vpp vpp-plugin-core vpp-plugin-dpdk vpp-dbg vpp-dev vpp-ext-deps vpp-api-python vpp-api-java -y
      SHELL
    end
  end

  #############
  # Client VM #
  #############
  (2231..2232).each do |host_id|
    vm_name  = "ClientVM-" + host_id.to_s

    config.vm.define vm_name do |srv6|
      srv6.vm.hostname = "client-#{host_id}"
      srv6.vm.box = "bento/ubuntu-18.04"
      srv6.vm.network "forwarded_port", guest: 22, host: host_id.to_i, host_ip: "127.0.0.1"

      case host_id
      when 2231 then
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db1::2",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2001"

      when 2232 then
        srv6.vm.network "private_network",
          auto_config: true,
          nic_type: "82540EM",
          ip: "2001:db10::2",
          netmask: "64",
          virtualbox__intnet: "srv6_seg2010"
      end

      srv6.vm.provider "virtualbox" do |vb|
        # Customize the amount of memory on the VM:
        vb.memory = "512"
      end

      srv6.vm.provision "shell", inline: <<-SHELL
        apt update
      SHELL
    end
  end

  ##############################
  ## Box provisioning        ###
  ##############################
  #config.vm.provision "ansible" do |ansible|
  #  # ansible.compatibility_mode = "2.0"
  #  ansible.config_file = "ansible.cfg"
  #  ansible.groups = {
  #    "vqfx10k" => ["vqfx1", "vqfx2" ],
  #    "vqfx10kpfe"  => ["vqfx1-pfe", "vqfx2-pfe"],
  #    "all:children" => ["vqfx10k", "vqfx10kpfe"]
  #  }
  #  ansible.playbook = "interfaces.yaml"
  #end

end
