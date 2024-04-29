# shorouk_Eid-
**# shorouk_Eid-**


## **description **
The WebServerSetup.yml Ansible playbook automates the installation and configuration of Apache HTTP Server on VM3. Below is an overview of the playbook structure and its functionality 

**Getting Started**  
Created 3 VMs on Jenkins, GitLab and Ansible using Azure Services  
Integration between Jenkins and GitLab '

# write bash Script on VM3

Bash script #!/bin/bash
# Create users
sudo useradd -m -s /bin/bash DevTeam
sudo useradd -m -s /bin/bash OpsTeam
# Create group
sudo groupadd webAdmins
# Add users to group
sudo usermod -aG webAdmins DevTeam
sudo usermod -aG webAdmins OpsTeam

![image](https://github.com/ShoroukEid/shorouk_Eid-/assets/111165635/8dba4703-6d9f-4e77-8ccc-692aeeedb02f)

**Write Ansible PlayBook.yaml.**

webServerSetup.yml
---
- name: Web Server Setup
  hosts: web_servers
  become: yes
  tasks:
    - name: Update yum package cache
      yum:
        update_cache: yes
    - name: Install Apache HTTP Server
      yum:
        name: httpd
        state: present

    - name: Enable Apache service
      systemd:
        name: httpd
        enabled: yes
        state: started

    - name: Allow HTTP traffic through UFW
      ufw:
        rule: allow
        #name: 'Apache Full'
        port: '80,443'
        proto: tcp

    #- name: Copy custom index.html file
     #copy:
        #src: /path/to/files/index.html
        #dest: /var/www/html/index.html
      #notify:
        #- restart httpd

  handlers:
    - name: restart httpd
      service:
        name: httpd
        state: restarted


**insatll and configure ansible in vm3**
create vm3 
anstall ansible and packjes 
create and write playbook.yml include tasks 
