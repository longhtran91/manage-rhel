# Manage RHEL hosts with users/groups

## Features

- setup_hosts: maintain ansible controlled hosts via `vars/managed_hosts.yaml`
- setup_identities: maintain ansible controlled users and groups via `vars/users_groups.yaml`

## setup_hosts:
### Example of `managed_hosts.yaml`
```sh
managed_hosts:
- hostname: ansible1
  ipv4: 172.16.1.241
  domain: example.com
- hostname: ansible2
  ipv4: 172.16.1.242
  domain: example.com
- hostname: ansible3
  ipv4: 172.16.1.243
  domain: example.com
- hostname: ansible4
  ipv4: 172.16.1.244
  domain: example.com
```
This is the list of hosts that the Ansible Control node will be manage. inventory file and /etc/hosts will be maintained according to this list

### ansible_user.yaml
```sh
ansible_username: ansible
ansible_password: password
```
This is the account will be setup for ansible.
> Consider using `ansible-vault` to encrypt sensitive data such as password.

## setup_identities:
### Example of `users_groups.yaml`
```sh
user_groups:
  - name: admin
    sudo: true
  - name: power_user
    sudo: true
  - name: marketing
  - name: it

users:
  - name: bill
    password: password
    groups: [admin, it]
  - name: ted
    password: password
    groups: [marketing]
  - name: tracy
    password: password
  - name: supersu1
    password: password
    sudo: true
  - name: supersu2
    password: password
    sudo: true
```
This is the list of users and groups that will be maintained by Ansible Control node. All users should be able to ssh into managed hosts
> Consider using `ansible-vault` to encrypt sensitive data such as password.
