# Ansible_lab
To run this lab need to download repository and run "vagrant up"

Vagrant create 3 VMs:

    control.example.com
    node1.example.com
    node2.example.com
  
After vagrant has started, need to create ssh key and copy to nodes

    ssh-keygen
    ssh-copy-id node1.example.com && ssh-copy-id node2.example.com

All ansible files from "Working_files" in repository copying to /home/ansible/lesson on control.example.com

Files list in "Working_files"

    hw3_task2.ftp - role for install ftp
    ansible.cfg   - ansible config
    inventory     - inventory file
    my_facts.fact - customs facts fro hw3_task1.yml
    pass_hw2.yml  - pass for hw2_task1.yml
    users.yml     - users list for hw2_task1.yml

Homeworks playbooks

    hw1_task1.yml - install and run web-server
  
    hw1_task2.yml - uninstall web-server
  
    hw1_task3.yml - change grub and apply config
	
    hw2_task1.yml - create users
    
    hw3_task1.yml - instal web-server with ansible features
    
    hw3_task2.yml - install and run ftp server
