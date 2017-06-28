Role Name
=========

ESXi_ssh configure ssh in our ESXi servers. Ignore shell warnings and Enable ssh server on boot

Requirements
------------

No requirements

Role Variables
--------------

No variables

Dependencies
------------

No dependencies

Example Playbook
----------------

This play is executed when update_mode var is "true" and ensure that role is up to date. By default update var is "false"

miquelMariano.ESXi_{{ role }} folder must be exist. If not, the playbook not found role and fails. You shoud make dir manually "mkdir /etc/ansible/my_role"

```yaml
###
###ESXi_config.yml
###		
- hosts: ansible
  user: root
  tasks:
    - name: Ensure that role are up to date
      command: ansible-galaxy install --force {{ item }}
      with_items:
        - miquelMariano.ESXi_{{ role  }}
      when:
        - update_mode | default(False)
      tags: update
      ignore_errors: yes

- hosts: "{{ servers }}:!localhost"
  user: root
  serial: 1
  roles:
   - role: miquelMariano.ESXi_{{ role  }}
~
~
~

```

Usage
------

```ssh
ansible-playbook playbooks/ESXi_config.yml -i inventory/ESXi --extra-vars "servers=servers_group1 role=ssh update_mode=true"
```


License
-------

BSD

Author Information
------------------

[miquelMariano.github.io](https://miquelMariano.github.io) | [Twitter](https://twitter.com/miquelMariano)

