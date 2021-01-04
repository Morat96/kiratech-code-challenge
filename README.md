# Kiratech Code Challenge
![ansible-lint](https://github.com/richiMarchi/kiratech-code-challenge/workflows/ansible-lint/badge.svg)

Ansible playbook for Kiratech challenge

## What it does

The `Vagrantfile` allows you to:

- Deploy 2 CentOS vms
- Run ansible playbook `playbook.yml`
  - Create and mount a 40GiB partition
  - Install Docker and Docker Compose
  - Setup Docker
- Run a simple serverspec test

## Prerequisites

- virtualbox
- vagrant
  - vagrant-hostsupdater plugin
  - vagrant-disksize plugin
  - vagrant-serverspec plugin
- ruby
- ansible

## How to deploy

### Brief setup

If you do not have an RSA SSH key pair yet, you can generate it with the following command:

`$ ssh-keygen -t rsa -N '' -f ~/.ssh/id_rsa -q`

Add this code to your `~/.ssh/config` file in order to handle vms in a more convenient way:

```
# For vagrant virtual machines
Host 192.168.33.* *.code-challenge
  StrictHostKeyChecking no
  UserKnownHostsFile=/dev/null
  User root
  LogLevel ERROR
```

Because of these lines:

- SSH won’t complain about non-matching keys for your ever-changing vagrant VMs
- SSH won’t try to remember and manage those keys via `~/.ssh/known_hosts`
- You won’t have to specify `root@…` every time
- SSH won't show warnings we are aware of

Install vagrant plugins:

`$ vagrant plugin install vagrant-disksize vagrant-hostsupdater vagrant-serverspec`

### Run the code

Simply type:

`$ vagrant up`
