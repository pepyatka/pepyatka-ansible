# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'ubuntu/trusty32'
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.ssh.forward_agent = true
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbooks/site.yml"
    ansible.sudo = true
    ansible.groups = {
      "pepyatka" => ["default"],
      "nginx" => ["default"],
      "redis" => ["default"]
    }
    ansible.extra_vars = {
      pepyatka_hostname: "localhost:8080",
      pepyatka_server_repo: "https://github.com/pepyatka/pepyatka-server.git",
      pepyatka_server_branch: "development",
      pepyatka_html_repo: "https://github.com/pepyatka/pepyatka-html.git",
      pepyatka_html_branch: "development"
    }
    ansible.raw_arguments = ENV['ANSIBLE_ARGS']
  end
end
