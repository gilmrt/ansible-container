Docker Server deployment
======================

Ansible playbook to update and configure Ubuntu, install docker and cdeploy portainer using automated Ansible deployment.

Requirements
-------------
* Ansible v2.9 or later  
* Collection Ansible Galaxy "ansible.posix"  

You might already have **ansible.posix** collection installed if you are using the ansible package. It is not included in ansible-core. To check whether it is installed, run:
```bash
ansible-galaxy collection list
```

To install it, use: 
```bash
ansible-galaxy collection install ansible.posix
```

Ubuntu
-------------
* Set timezone  
* Update Ubuntu  
* Disable cloud-init  

Docker
-------------
* Install Docker
* Configure docker daemon
* Create additional user and group *(optional)*

Portainer
-------------
* Install Portainer from docker-compose
* Create dedicated network *(optional)*

Playbook : remote.yml 
--------------
**Description of the playbook**  
This playbook is dedicated to run remotely  
You need to have ssh access using ssh key configured

**Variables**  

| Variable | Description | Default |  
|---|---|---|  
| timezone  | Define the local timezone | Europe/Paris |  
| ubuntu__swapiness | vm.swapiness value | 60 |  
| ubuntu__vfs_cache_pressure | vfs_cache_pressure value | 100 |  
| ubuntu__user_name | Additional ubuntu user | dockerbot |  
| ubuntu__user_group | Additional ubuntu user group | dockerbot |  
| ubuntu__user_uid | Additional ubuntu user uid |  |  
| ubuntu__user_gid | Additional ubuntu user gid |  |  
| ubuntu__user_home | Additional ubuntu user home creation | yes |  
| ubuntu__user_shell | Additional ubuntu user shell | /bin/bash |  
| docker__path | Path to the Docker data (config, volumes,...) | /docker |  
| portainer__network | Dedicated docker network for containers | home |  
| duplicati__path | Duplicati restore path | /mnt/backup |  
| duplicati__passphrase | Duplicati restore passphrase |  |  
| duplicati__report | Duplicati restore report | false |  

**Remote usage**  
```bash
ansible-playbook -i inventories/<ENV>/ remote.yml -u <USER>
```
**Local usage**  
```bash
ansible-playbook local.yml
```
**Tag usage** 
```bash
ansible-playbook -i inventories/<ENV>/ remote.yml -u <USER> --limit <HOST> --tags <CONFIG_TAG>
```

**Tips**  
You can hide skipping tasks using an predefined environment variable `ANSIBLE_DISPLAY_SKIPPED_HOSTS=no`
```bash
ANSIBLE_DISPLAY_SKIPPED_HOSTS=no ansible-playbook -i inventories/<ENV>/ remote.yml -u <USER>
```


Tags
----------------
- install
- configure


Encryption (ansible-vault)
--------------
To encrypt a file use the following command:
```bash
ansible-vault encrypt path/to/filename.ext
```

To decrypt a file:
```bash
ansible-vault decrypt path/to/filename.ext
```

Decrypt files during playbook run
```bash
ansible-playbook --ask-vault-pass -i inventories/<ENV>/ remote.yml -u <USER>
```

Maintainer
----------
Gilles Martin  


License
-------
BSD
