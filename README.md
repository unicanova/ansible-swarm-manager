# Documentation

The role initializes docker swarm cluster and connects the swarm manager to it

+ [Quickstart](#Quickstart)
+ [Example requiremetns.yml file](#Ex1);
+ [Example host file](#Ex2);
+ [Examoke vars/main.yml](#Ex3);
+ [Playbook variables](#Table1);


## <a name="Quickstart"></a> Quickstart

[Install ansible](http://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) on the your host
Install python on the servers, if necessary  
You need to create a [requirements.yml](#Ex1) file and write down what roles are required in it. Then install roles from this file.
Install required rolles:  
```sh
$ ansible-galaxy install -r requirements.yml
```
Clone this repository in your directory:

```sh
$ git clone https://github.com/unicanova/ansible-swarm-manager
$ cd ansible-users
```
Specify host addresses in the file /etc/ansible/hosts.  
Create a [site.yml](#Ex3) file, where you can specify where you want initialize the swarm cluster and connect the swarm manager to it.  
In the playbook site.yml you can override varibales according to the [table](#Table1), if necessary.  

Execute command:  

```sh
$ ansible-playbook site.yml -b --extra-vars "ansible_sudo_pass=yourPassword"
```
#### <a name="Ex1"></a> Example requirements.yml:
```sh
- src: https://github.com/unicanova/ansible-swarm-manager
  version: master
  name: ansible-swarm-manager
```

#### <a name="Ex2"></a> Example hosts file:

```sh
[jenkinsmaster]
192.168.122.123 ansible_ssh_port=22 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

[jenkinslave]
192.168.122.77 ansible_ssh_port=22 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```
#### <a name="Ex3"></a> Example site.yml:
```sh
- hosts: test
  roles:
    - ansible-swarm-manager
  vars:
    - swarm_manager_init_host: services.multicast-media.com
```

#### <a name="Table1"></a> Playbook variables
| Variable name | Variables description |
| ------------- | --------------------- |
| swarm_manager_init_host | host on which you need to initialize the swarm manager |
