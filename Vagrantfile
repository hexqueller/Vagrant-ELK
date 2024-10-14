Vagrant.configure("2") do |config|

    machines = [
      { name: "elk-master", ip: "10.0.0.50" }
    ]
  
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "vagrant.yml"
    end
  
    machines.reverse.each do |machine|
        config.vm.define machine[:name] do |node|
          node.vm.box = "debian/bookworm64"
          node.vm.hostname = machine[:name]
          node.vm.network "public_network", bridge: "eno1", ip: machine[:ip], dev: "eno1"
          node.vm.provider "virtualbox" do |vb|
            vb.memory = "4096"
            vb.cpus = 4
          end
      end
    end
  end
