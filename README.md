Provision Promox VMs
=========

A project to deploy Red Hat subscribed virtual machines to a desired proxmox host via Ansible

Requirements
------------
---
##### ENVIRONMENT VARIABLE REQUIREMENTS
- export PROXMOX_PASSWORD='*******'
- export PROXMOX_URL='proxmox.example.com'
- export PROXMOX_USER='jdoeo@pam'
- export REDHAT_PASS='******'
- export REDHAT_USER='jdoe@duck.com'  

##### PROXMOX REQUIREMENTS
- Working proxmox environment
- A defined directory on proxmox server for qcow images 
- A valid proxmox user/pass with admin rights via api access from Ansible controller
- A valid proxmox user/pass with admin rights via ssh access from Ansible controller

##### ANSIBLE REQUIREMENTS
- The community.general collection is installed
- The ansible.posix collection is installed
- Path for the private_key_file variable in the included ansible.cfg file is correct. 
##### PLAYBOOK REQUIREMENTS
- A desired cloud-init user/pass for provisioning
- A valid ssh key to be use for distributing to hosts via cloud-init
- A valid Red Hat account with access to subscriptions

Dependencies
------------

None

Example Syntax 
----------------
### To provision virtual machines:

```
    ansible-playbook site.yml
```
### To unsubscribe and deprovision virtual machines
```
    ansible-playbook site.yml --tags never -e clean=true
```
### To deprovision virtual machines 
```
    ansible-playbook site.yml --tags never 
```
---
---
Example Playbook 
----------------

```
---
- hosts: localhost
  gather_facts: false
  collections:
       community.general
  pre_tasks:
     - name: Ensure netaddr python module is installed
       ansible.builtin.pip:
           name: netaddr
           extra_args: --user 
  roles:
     - provision_proxmox_vms
```

License
-------

MIT

Author Information
------------------

Randy Romero  
binbashroot@duck.com


