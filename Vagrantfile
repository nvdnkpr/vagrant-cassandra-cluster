# -*- mode: ruby -*-
# vi: set ft=ruby :

boxes = [
  { :name => :node0, :ip => '10.200.1.200', :cpus =>4, :memory => 1024 },
  { :name => :node1, :ip => '10.200.1.201', :cpus =>4, :memory => 1024 },
  { :name => :node2, :ip => '10.200.1.202', :cpus =>4, :memory => 1024 } 
]


Vagrant.configure("2") do |config|

  boxes.each do |opts|
    config.vm.define opts[:name] do |config|

      config.vm.hostname = "cassandra.%s" % opts[:name].to_s

      config.vm.synced_folder "./data", "/vagrant_data"

      config.vm.box = "precise64"
      config.vm.network :private_network, ip: opts[:ip]

      config.vm.provision :shell, :inline => "hostname cassandra.%s" % opts[:name].to_s
      config.vm.provision :shell, :inline => "cp -fv /vagrant_data/hosts /etc/hosts"

      config.vm.provider :virtualbox do |vb|
        vb.name = "storm.%s" % opts[:name].to_s
        vb.customize ["modifyvm", :id, "--memory", opts[:memory]]
        vb.customize ["modifyvm", :id, "--cpus", opts[:cpus] ] if opts[:cpus]
      end

    end
  end

end
