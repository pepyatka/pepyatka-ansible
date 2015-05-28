# Provisioning and deploying pepyatka-server
## Installing ansible

    apt-get install python-dev gcc
    apt-get install python-pip
    pip install ansible

Minimal required ansible version is 1.9.
More installation options: http://docs.ansible.com/intro_installation.html#installing-the-control-machine

### Configuring
I recommend to add the following alias in your .bashrc:

    alias play=ansible-playbook

Assume play=ansible-playbook down below.

## Provisioning pepyatka
Copy dev.template to dev, replace placeholders with your data and run:

    play -i dev playbooks/site.yml [-s]

Flag '-s' is optional, use it if remote user on your server is anything other than root.
You can add --ask-sudo-pass flag and ansible will ask sudo password in runtime if that user does not have passwordless sudo.

### Provisioning locally
Install ansible, clone this repo, replace placeholders in inventory 'local' with your data and run as root:

    ansible-playbook -i local playbooks/site.yml --connection=local

### Boostrap
You can boostrap a VM (e.g. an instance in Digital Ocean) with ansible. It will install everything and configure a cron job which will poll git repos for changes and redeploy pepyatka if needed.

Copy dev.template to dev, replace placeholders with your data and run:

    play -i dev playbooks/boostrap.yml [-s]

See "Provisioning pepyatka" for more details.

## Ad-hoc commands
Check if all servers are up:

    ansible -i dev all -m ping

Check status of nginx:

    ansible -i dev nginx -a "service nginx status"

## Development environment with vagrant
It's very easy to get a live-like VM with the help of vagrant and ansible.
Installing vagrant: https://www.vagrantup.com/downloads.html

Update Vagrantfile to point to your repositories, specify your feature branches and

    vagrant up

When you pushed some changes:

    ANSIBLE_ARGS='-tpepyatka' vagrant provision

To run full provisioning again:

    vagrant provision
