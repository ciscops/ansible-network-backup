network-config
=========

This role backs up the configuration of a network device into a git repository.

The file is backed up to `{{ net_backup_dir }}/{{ inventory_hostname }}.cfg`


Requirements
------------

Currently supports:
- ios
- nxos

Role Variables
--------------

- `network_backup_dir`: The dictory where the backups will be placed.
- `network_backup_repository`: The git repository that will be use to store the backups

Dependencies
------------

None

Example Playbook
----------------

    - hosts: network
      gather_facts: no
      tasks:
        - include_role:
            name: network-config
          vars:
            network_backup_repository: 'git@github.com:ismc/configs.git'
            net_backup_dir: "{{ lookup('env', 'PWD') }}/backups"

The playbook can be run to either backup or check for changes:

    ansible-playbook -i hosts net-backup.yml

The playbook can be run to display the differences found between the saved config and the running config:

    ansible-playbook --diff -i hosts net-backup.yml



License
-------

GPL-3.0
