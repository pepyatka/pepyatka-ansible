# Provisioning and deploying pepyatka-server
## Installing ansible
### CentOS

    sudo yum install ansible

### Debian/Ubuntu

    sudo apt-get install software-properties-common
    sudo apt-add-repository ppa:ansible/ansible
    sudo apt-get update
    sudo apt-get install ansible

### Mac OSX

    brew update
    brew install ansible

### Configuring
I recommend to add the following alias in your .bashrc:

    alias play=ansible-playbook

Assume play=ansible-playbook down below.

## Provisioning pepyatka server

    play -i staging playbooks/site.yml -s

## Ad-hoc commands
Check if all servers are up:

    ansible -i hosts all -m ping

Check status of the redis service:

    ansible -i hosts redis -a "systemctl status redis"

## Development environment with vagrant
It's very easy to get a live-like VM with the help of vagrant and ansible.
Installing vagrant: https://www.vagrantup.com/downloads.html

Update Vagrantfile to point to your repositories, specify your feature branches and

    vagrant up

When you pushed some changes:

    ANSIBLE_ARGS='-tpepyatka' vagrant provision

To run full provisioning again:

    vagrant provision
