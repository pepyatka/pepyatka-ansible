# Provisioning and deploying pepyatka-server
## Installing ansible

    sudo pip install ansible

Minimal required ansible version is 1.9.
More installation options: http://docs.ansible.com/intro_installation.html#installing-the-control-machine

### Configuring
I recommend to add the following alias in your .bashrc:

    alias play=ansible-playbook

Assume play=ansible-playbook down below.

## Provisioning pepyatka server

    play -i prod playbooks/site.yml -s

## Ad-hoc commands
Check if all servers are up:

    ansible -i prod all -m ping

Check status of the redis service:

    ansible -i prod pepyatka -a "service nginx status"

## Development environment with vagrant
It's very easy to get a live-like VM with the help of vagrant and ansible.
Installing vagrant: https://www.vagrantup.com/downloads.html

Update Vagrantfile to point to your repositories, specify your feature branches and

    vagrant up

When you pushed some changes:

    ANSIBLE_ARGS='-tpepyatka' vagrant provision

To run full provisioning again:

    vagrant provision
