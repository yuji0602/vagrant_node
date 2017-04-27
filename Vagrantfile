# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'ubuntu/xenial64'
  config.vm.hostname = 'vagrantNode'

  config.vm.network :private_network,
                    ip: '192.168.100.30'
  config.vm.synced_folder './', '/vagrant'

  config.vm.provider 'virtualbox' do |v|
    v.memory = 2048
    v.customize ['modifyvm', :id, '--paravirtprovider', 'kvm']
  end

  config.vm.provision 'shell',
                      inline: 'apt-get update && apt-get upgrade -y && apt-get install -y build-essential libssl-dev libffi-dev libyaml-dev python-dev python-pip language-pack-ja ntp ntpdate'

  config.vm.provision 'shell',
                      inline: 'pip install --upgrade pip setuptools ansible markupsafe'
  config.vm.provision 'shell',
                      inline: "ansible-playbook -c local -i 'localhost,' /vagrant/ansible/playbook/main.yml",
                      privileged: false

  Encoding.default_external = 'UTF-8'
end
