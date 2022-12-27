# frozen_string_literal: true

K3S_TOKEN = ''
K3S_URL = 'https://192.168.56.10:6443'

machines = [
  {
    hostname: 'nodea',
    ip: '192.168.56.10',
    memory: '4096',
    cpus: 4,
    script: 'curl -sfL https://get.k3s.io | sh -'
  },
  {
    hostname: 'nodeb',
    ip: '192.168.56.11',
    memory: '2048',
    cpus: 2,
    script: "curl -sfL https://get.k3s.io | K3S_TOKEN=#{K3S_TOKEN} K3S_URL=#{K3S_URL} sh -"
  }
]

Vagrant.configure('2') do |config|
  machines.each do |options|
    config.vm.define options.fetch(:hostname) do |node|
      node.vm.box = 'hashicorp/bionic64'

      node.vm.hostname = options.fetch(:hostname)

      node.vm.provider 'virtualbox' do |v|
        v.memory = options.fetch(:memory)
        v.cpus = options.fetch(:cpus)
      end

      node.vm.network :private_network, ip: options.fetch(:ip)

      node.vm.provision 'shell', inline: options.fetch(:script)
    end
  end
end
