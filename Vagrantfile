# -*- mode: ruby -*-
# vim: set ft=ruby :
MACHINES = {
:inetRouter => {
        :box_name => "centos/7",
        :box_version => "2004.01",
        #:public => {:ip => '10.10.10.1', :adapter => 1},
        :net => [
                   #{ip: '192.168.255.1', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "router-net"},
                   {adapter: 2, auto_config: false, virtualbox__intnet: "router-net"},
                   {adapter: 3, auto_config: false, virtualbox__intnet: "router-net"},
                   {ip: '192.168.56.10',adapter:8},
                ]
  },
  :centralRouter => {
        :box_name => "centos/7",
        :box_version => "2004.01",
        :net => [
                   {adapter: 2, auto_config: false, virtualbox__intnet: "router-net"},
                   {adapter: 3, auto_config: false, virtualbox__intnet: "router-net"},
                   {ip: '192.168.255.9', adapter: 6, netmask: "255.255.255.240", virtualbox__intnet: "office1-central"},
                   {ip: '192.168.56.11', adapter: 8},
                ]
  },
  :office1Router => {
    :box_name => "centos/7",
    :box_version => "2004.01",
    :net => [
      {ip:'192.168.255.10', adapter:2, netmask: '255.255.255.252', virtualbox__intnet: "office1-central"},
      {adapter:3, auto_config: false, virtualbox__intnet: "vlan1"},
      {adapter:4, auto_config: false, virtualbox__intnet: "vlan1"},
      {adapter:5, auto_config: false, virtualbox__intnet: "vlan2"},
      {adapter:6, auto_config: false, virtualbox__intnet: "vlan2"},
      {ip: '192.168.56.20', adapter:8},
    ]
  },
  :testClient1 => {
    :box_name => "centos/7",
    :box_version => "2004.01",
    :net => [
      {adapter:2, auto_config: false, virtualbox__intnet: "testLAN"},
      {ip: '192.168.56.21', adapter:8},
    ]
  },
  :testServer1 => {
    :box_name => "centos/7",
    :box_version => "2004.01",
    :net => [
      {adapter:2, auto_config: false, virtualbox__intnet: "testLAN"},
      {ip: '192.168.56.22', adapter:8},
    ]
  },
  :testClient2 => {
    :box_name => "centos/7",
    :box_version => "2004.01",
    :net => [
      {adapter:2, auto_config: false, virtualbox__intnet: "testLAN"},
      {ip: '192.168.56.31', adapter:8},
    ]
  },
  :testServer2 => {
    :box_name => "centos/7",
    :box_version => "2004.01",
    :net => [
      {adapter:2, auto_config: false, virtualbox__intnet: "testLAN"},
      {ip: '192.168.56.32', adapter:8},
    ]
  },
  
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

    config.vm.define boxname do |box|

        box.vm.box = boxconfig[:box_name]
        box.vm.host_name = boxname.to_s
        box.vm.provider :virtualbox do |vb|
          vb.customize ["modifyvm", :id, "--memory", "192"]
          vb.customize ["modifyvm", :id, "--cpus", "1"]
        end
        boxconfig[:net].each do |ipconf|
          box.vm.network "private_network", ipconf
        end
        
        if boxconfig.key?(:public)
          box.vm.network "public_network", boxconfig[:public]
        end

        box.vm.provision "shell", inline: <<-SHELL
          mkdir -p ~root/.ssh
                cp ~vagrant/.ssh/auth* ~root/.ssh
        SHELL
    end
  end
end