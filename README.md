[![published](https://static.production.devnetcloud.com/codeexchange/assets/images/devnet-published.svg)](https://developer.cisco.com/codeexchange/github/repo/ciscops/ansible-network-backup)

# Ansible Network Backup

This role backs up the configuration of a network device into a git repository.

The file is backed up to the directory specified in `network_backup_dir`.  A git repo is used when
`network_backup_repository` is specified.


## Requirements


Currently supports:
* Cisco IOS XE
* Cisco NX OS
* Cisco ASA

## Role Variables


* `network_backup_repository`: The git repository that will be use to store the backups
  * _Backups will not be pushed to git when `network_backup_repository` is not specified_
* `network_backup_dir`: The directory where the backups will be placed. Default: `"{{ playbook_dir }}/backups"`
  * _`network_backup_dir` will be created when it does not exist_
* `git_name`: Set the user's git name when not otherwise specified
* `git_email`: Set the user's git email when not otherwise specified

## Dependencies

None

## Cloning

Adding without the `ansible-` prefix:

`git clone git@github.com:ciscops/ansible-network-backup.git network-backup`

Adding as a submodule:

`git submodule add git@github.com:ciscops/ansible-network-backup.git network-backup`

## Example Playbook


```yaml
- hosts: network
  gather_facts: no
  connection: network_cli
  tasks:
    - include_role:
        name: network-backup
      vars:
        network_backup_repository: 'git@github.com:repo/backups.git'
```

## License


[CISCO SAMPLE CODE LICENSE](./LICENSE).
