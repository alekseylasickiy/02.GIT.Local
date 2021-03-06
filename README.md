# 05. Ansible start

### Create host file:
```bash
[jump]
 bastion ansible_host=178.124.206.53
 
 [ec:children]
 ec_centos
 ec_ubuntu
 
 [ec_centos]
 host1 ansible_host=192.168.203.37
 host3 ansible_host=192.168.203.39
 
 [ec_ubuntu]
 host2 ansible_host=192.168.203.38
 host4 ansible_host=192.168.203.40
```
[hosts](./hosts)

### Create ssh config file:
```bash
###############################
 # EC HTP
 ###################################
 # EC HTP
 Host ec_bastion
         User jump_sa
         HostName 178.124.206.53
 Host  192.168.203.37 192.168.203.38 192.168.203.39 192.168.203.40
         ProxyJump ec_bastion
```
[ssh config](./config)

### Edit ansible config file:

[ansible.cfg](./ansible.cfg)


### Check [ec] hosts:
```bash
ansible -m ping ec -u root
```
#### Output:
```bash
host3 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
host1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
host2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
host4 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

### Print out host names and IP
```bash
ansible -u root ec -m shell -a 'hostname -A && hostname -I'
```
[hostnames/ip](./host_names_ip)

### Upgrade packages
#### For Ubuntu servers use command:
```bash
ansible ec_ubuntu -u ansibleusr -m shell -a "sudo yum -y upgrate"
```
[ec_ubuntu output](./ec_ubunu_upgrade)

#### For Centos servers use command:
```bash
ansible ec_centos -u ansibleusr -m shell -a "sudo yum -y update"
```
[ec_centos output](./ec_centos_upgrade)

