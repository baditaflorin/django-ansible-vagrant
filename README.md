# django-ansible-vagrant

### Instructions

1. Install [Vagrant](https://www.vagrantup.com/downloads.html) and [Ansible](http://docs.ansible.com/ansible/intro_installation.html)

2. Set `application_name` in ansible/vagrant.yml

3. Provision the VM with `vagrant up`

4. SSH into the VM with `vagrant ssh`

5. Create a django project with the `application_name` used in vagrant.yml:
`django-admin startproject application_name`

6. Use `runserver` to start the Django server

7. Access the django server at http://192.168.4.23/

