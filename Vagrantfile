# -*- mode: ruby -*-
# vi: set ft=ruby :
$hostsfile_update = <<-'SCRIPT'
echo -e '192.168.56.110 control.example.com control\n192.168.56.111 node1.example.com node1\n192.168.56.112 node2.example.com node2' >> /etc/hosts
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config && systemctl restart sshd
SCRIPT

$all_nodes = <<-'SCRIPT'
useradd ansible
echo password | passwd --stdin ansible
echo "ansible ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/ansible
SCRIPT

$control_node = <<-'SCRIPT'
yum install -y epel-release
yum install -y ansible
ansible --version 
su - ansible

SCRIPT

$control_node_copy_files = <<-'SCRIPT'
mkdir /home/ansible/lesson/
cp -a /tmp/temp/* /home/ansible/lesson/
chown -R ansible:ansible /home/ansible/
rm -rf /tmp/temp/
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.define "control", primary: true do |control|
    control.vm.box = "centos/8"
    control.vm.hostname = "control.example.com"
    control.vm.network "forwarded_port", guest: 80, host: 8080
    control.vm.network "private_network", ip: "192.168.56.110"
	control.vm.provision "file", source: "./", destination: "/tmp/temp/"
    control.vm.provision "shell", inline: $hostsfile_update
    control.vm.provision "shell", inline: $all_nodes
    control.vm.provision "shell", inline: $control_node
    control.vm.provision "shell", inline: $control_node_copy_files
    control.vm.provider "virtualbox" do |v|
    config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--audio", "none"]
    end
 	v.memory = 4096
	v.cpus = 2
    end
  end

  config.vm.define "node1" do |node1|
    node1.vm.box = "centos/8"
    node1.vm.hostname = "node1.example.com"
    node1.vm.network "private_network", ip: "192.168.56.111"
    node1.vm.provision "shell", inline: $hostsfile_update
    node1.vm.provision "shell", inline: $all_nodes
    config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--audio", "none"]
    end
  end

  config.vm.define "node2" do |node2|
    node2.vm.box = "centos/8"
    node2.vm.hostname = "node2.example.com"
    node2.vm.network "private_network", ip: "192.168.56.112"
    node2.vm.provision "shell", inline: $hostsfile_update
    node2.vm.provision "shell", inline: $all_nodes
    config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--audio", "none"]
    end
  end

end
