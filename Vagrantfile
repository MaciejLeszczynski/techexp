# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "centos/7"

   config.vm.define "node1" do |node1|
    node1.vm.box = "centos/7"
    node1.vm.network  "private_network", dev: "ovirtmgmt", mode: "bridge", type: "bridge", ip: "172.168.100.10"
  end

   config.vm.define "node2" do |node2|
    node2.vm.box = "centos/7"
    node2.vm.network  "private_network", dev: "ovirtmgmt", mode: "bridge", type: "bridge", ip: "172.168.100.11"
  end

   config.vm.define "node3" do |node3|
    node3.vm.box = "centos/7"
    node3.vm.network  "private_network", dev: "ovirtmgmt", mode: "bridge", type: "bridge", ip: "172.168.100.12"
  end

  config.vm.provider :libvirt do |libvirt|
    libvirt.cpus = 4
    libvirt.memory = 8192
  end

  config.ssh.forward_agent    = true
  config.ssh.insert_key       = false
  config.ssh.private_key_path =  ["~/.vagrant.d/insecure_private_key","~/.ssh/id_rsa"]
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
  config.vm.provision "shell", inline: <<-EOC
    sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
    sudo systemctl restart sshd.service
    echo "finished"
  EOC
end
