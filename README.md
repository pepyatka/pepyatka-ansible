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
