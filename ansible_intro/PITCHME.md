## Ansible 介绍

* It's a **simple automation language** that can perfectly describean IT application infrastructure in Ansible Playbooks.

* It's an **automation engine** that runs Ansible Playbooks.

---
### Ansible 优势 

![](https://ws4.sinaimg.cn/large/006tNc79ly1fyz138gflaj31tl0u0wjh.jpg)

---
### Ansible 安装
<br>
<br>
<br>

```
# install ansible using pip

pip install ansible


```

---
### Ansible Inventory file

* Define how ansible will interact with remote hosts
<br>
* Define logical group of managed nodes
<br>
* Default location: /etc/ansible/hosts
<br>
* Ini format

---
### Ansible Inventory file
* ansible_connection: local, ssh or paramiko
<br>
* ansible_ssh_host: the name of the host to connect to 
<br>
* ansible_ssh_port: the ssh port if not 22
<br>
* ansible_ssh_user: the ssh user name to use
<br>
* ansible_ssh_pass: the ssh password to use
<br>
* ansible_ssh_private_key_file: private key file used by ssh

---
### Ansible Inventory file

<br>
```
localhost ansible_connection=local

[webservers]
web[1:5].example.com ansible_connection=ssh ansible_ssh_user=webadmin

[dbservers]
db[1,2].example.com ansible_connection=ssj ansible_ssh_user=dbadmin

[allservers: children]
webservers
dbservers


```
<br>


---
###  Ansible Playbook 
<br>
* expressed in YAML language
<br>
* composed of one or more "palys" in a list
<br>
* allowing multi-machine deployments orchestration 
<br>

---

<br>
<br>
```
- host: webservers
  vars:
    http_port: 80
    max_clients: 200
  tasks:
  - name: ensure apache is at the latest version
    yum: pkg=httpd state=latest
  - name: write the apache config file
    template: src=/srv/httpd.j2 dest=/etc/httpd/conf


```

@[1](host 定义了这个块执行的目标host)
@[2-4](定义一些变量)
@[5-9](定义了这个块需要对目标host执行的任务)
@[6-7](定义一个任务的name,还有需要调用的module)

---
