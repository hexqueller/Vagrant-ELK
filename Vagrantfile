Vagrant.configure("2") do |config|

  machines = [
    { name: "local-repo", ip: "10.0.0.50" },
    { name: "enode1", ip: "10.0.0.51" },
    { name: "enode2", ip: "10.0.0.52" },
    { name: "enode3", ip: "10.0.0.53" },
    { name: "lnode", ip: "10.0.0.54" },
    { name: "knode", ip: "10.0.0.55" }
  ]

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant.yml"
  end

  machines.each do |machine|
    config.vm.define machine[:name] do |node|
      node.vm.box = "debian/bookworm64"
      node.vm.hostname = machine[:name]
      node.vm.network "public_network", bridge: "eno1", ip: machine[:ip], dev: "eno1"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.cpus = 1
      end
    end
  end
end
