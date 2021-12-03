# Ansible lab with the docker container (debian version)

### 01. Generate the ssh-keys and build the ubuntu-lab image
```sh
ssh-keygen -f keycontainer
docker build -t ubuntu-lab .
```

### 02. Start 3 instance of the ansible client's with different hostname
```sh
docker container run -d --name=host01 ubuntu-lab
docker container run -d --name=host02 ubuntu-lab
docker container run -d --name=host03 ubuntu-lab
```
### 03. Get the ip address of the ansible client's
```sh
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name_or_id
```

### 04. Prepare the inventory file like below
```sh
cat inventory
target1  ansible_host=172.17.0.2 ansible_ssh_private_key_file=/home/anjon/.ssh/keycontainer
target2  ansible_host=172.17.0.3 ansible_ssh_private_key_file=/home/anjon/.ssh/keycontainer
target3  ansible_host=172.17.0.4 ansible_ssh_private_key_file=/home/anjon/.ssh/keycontainer
```

### 05. Now write the simple ping playbook 
```sh
cat ping_play.yml
---
- name: Deploy a web application
  hosts: all
  become: true
  tasks:
  - name: Try Ping
    ansible.builtin.ping:

```

### 06: Run the playbook for test the connectivity
```sh
ansible-playbook -i inventory ping_play.yml
``` 
