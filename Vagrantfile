# По умолчанию устанавливается OpenSearch, но можно выбрать Elasticsearch
# export STACK=ElasticSearch ( только на время терминальной сессии )

STACK = ENV['STACK'] || 'OpenSearch'

elastic_search_nodes = [
  { name: "enode1", ip: "10.0.0.51" },
  { name: "enode2", ip: "10.0.0.52" },
  { name: "enode3", ip: "10.0.0.53" },
  { name: "lnode", ip: "10.0.0.54" },
  { name: "knode", ip: "10.0.0.55" }
]

open_search_nodes = [
  { name: "onode1", ip: "10.0.0.61" },
  { name: "onode2", ip: "10.0.0.62" },
  { name: "onode3", ip: "10.0.0.63" },
  { name: "dnode", ip: "10.0.0.64" }
]

nodes = case STACK
        when 'ElasticSearch'
          elastic_search_nodes
        when 'OpenSearch'
          open_search_nodes
        else
          raise "Неправильное значение переменной STACK: #{STACK}"
        end

Vagrant.configure("2") do |config|

  config.vm.define "local-repo" do |node|
    node.vm.box = "debian/bookworm64"
    node.vm.hostname = "local-repo"
    node.vm.network "public_network", bridge: "eno1", ip: "10.0.0.50", dev: "eno1"
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 1
    end
  end

  nodes.each do |machine|
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

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant.yml"
  end
end