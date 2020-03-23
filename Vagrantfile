IMAGE_NAME = "centos/7"
N = 2

Vagrant.configure("2") do |config|
      
    config.vm.define "master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.hostname = "master.example.com"
        master.vm.network "private_network", ip: "192.168.7.2"
        master.vm.hostname = "master"
        master.vm.provider "virtualbox" do |v|
          v.name = "master"
          v.memory = 2048
          v.cpus = 2
          end
    end

    (1..N).each do |i|
        config.vm.define "node#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.hostname = "node#{i}.example.com"
            node.vm.network "private_network", ip: "192.168.7.#{i+2}"
            node.vm.hostname = "node#{i}"
            node.vm.provider "virtualbox" do |v|
              v.name = "node#{i}"
              v.memory = 1024
              v.cpus = 1      
            end
        end
    end
end
