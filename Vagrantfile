# vi: ft=ruby

VAGRANTFILE_API_VERSION = '2'
ROLE_NAME = 'wordpress'

hosts = [
  { maintainer: 'bertvv', distro: 'centos72', ip: '192.168.56.4' },
  { maintainer: 'bertvv', distro: 'fedora25', ip: '192.168.56.5' }
]

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define 'db' do |node|
    node.vm.box = 'bertvv/centos72'
    node.vm.hostname = 'db'
    node.vm.network :private_network, ip: '192.168.56.99'
  end

  hosts.each do |host|
    host_name = host[:distro] + '-' + ROLE_NAME

    config.vm.define host_name do |node|
      node.vm.box = host[:maintainer] + '/' + host[:distro]
      node.vm.hostname = host_name
      node.vm.network :private_network, ip: host[:ip]
    end
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'test.yml'
  end
end
