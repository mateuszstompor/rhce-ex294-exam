# 16. Roles - Solution

1. Go to the `/home/automation/plays` and create a folder for roles
```
mkdir roles
```
If you configured ansible correctly while solving the first exercise role that you are going to create will be detected by playbook automatically 

2. Change CWD to newly created directory and initate skeleton for the role
```
ansible-galaxy role init apache
```
3. Remove all folders different than `tasks` or `meta`
4. Edit `tasks/main.yml` to look as follows
```yml
---
- name: Install required packages
  yum:
    name:
    - httpd
    - firewalld
    state: present
- name: Allow required ports
  firewalld:
    permanent: true
    state: enabled
    port: "{{ item }}"
    immediate: true
  with_items:
  - 80/tcp
  - 443/tcp
- name: Ensure that services are started on boot
  service:
    name: "{{ item }}"
    state: started
    enabled: true
  with_items:
  - httpd
  - firewalld
- name: Prepare index page
  copy:
    content: "Welcome, you have connected to {{ ansible_facts.fqdn }}\n"
    dest: /var/www/html/index.html
```
5. Edit `meta/main.yml` as below
```yml
galaxy_info:
  author: Mateusz Stompór
  description: This role sets up webserver
  license: MIT
  min_ansible_version: 2.9
  galaxy_tags: []
dependencies: []
```
5. Finally create the playbook at `/home/automation/plays/apache.yml` with following content:
```yml
---
- hosts: webservers
  roles:
  - role: apache
    become: true
```

To run the playbook go to `/home/automation/plays` and call
```bash
ansible-playbook apache.yml
```