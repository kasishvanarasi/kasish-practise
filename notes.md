--- 
- name: uninstall httpd application
  hosts: all
  become: true
  tasks:
# stop httpd application service
  - name: stop service httpd
    service:
      name: httpd
      state: stopped
    when: ansible_os_family=="RedHat"
 # uninstall httpd application
  - name: uninstall httpd
    yum:
      name: httpd
      state: removed
    when: ansible_os_family=="RedHat"
 # stop apache2 application service
  - name: stop service apache2
    service:
      name: apache2
      state: stopped
    when: ansible_os_family=="Debian"           
   # install apache2 application
  - name: install apache2 
    apt:
      name: apache2
      state: removed
    when: ansible_os_family=="Debian"