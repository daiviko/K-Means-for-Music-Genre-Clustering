nodes = ["node0","node1","node2"]


Vagrant.configure("2") do |config|
  config.vm.box = "booz-allen-hamilton/centos-6.6-minimal"

  nodes.each do |node|
    config.vm.define node do |node|
      node.vm.box = "booz-allen-hamilton/centos-6.6-minimal"
    end
    config.vm.provision "ansible" do |ansible|
      ansible.groups = {
        "dns" => [nodes[0]],
        "dns-pri" => [nodes[0]],
        "dns-sec" => [nodes[1]],
        "ldap" => [nodes[1],nodes[2]],
        "ldap-pri" => [nodes[1]],
        "ldap-sec" => [nodes[2]],
        "krb" => [nodes[1], nodes[2]],
        "krb-pri" => [nodes[1]],
        "krb-sec" => [nodes[2]],
        "ambari" => [nodes[2], nodes[0]],
        "postgres" => [nodes[0], nodes[1]],
        "postgres-pri" => [nodes[0]],
        "postgres-sec" => [nodes[1]],
        "nfs" => [nodes[2]],
        "namenodes" => [nodes[0],nodes[1]],
        "datanodes" => [nodes[0],nodes[1],nodes[2]],
        "nodemanagers" => [nodes[0],nodes[1],nodes[2]],
        "resourcemanager" => [nodes[1],nodes[2]],
        "knox" => [nodes[2],nodes[0]],
        "metastore" => [nodes[1],nodes[2]],
        "webhcat" => [nodes[2],nodes[0]],
        "ganglia" => [nodes[0]],
        "nagios" => [nodes[1]]
      }
      ansible.playbook = "apollo-playbook.yml"
      ansible.extra_vars = {
        cluster_domain: "apollo-test.bah.com",
        ip4_cluster_subnet: ""
      }
    end
  end  
end
