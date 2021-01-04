require_relative './scripts/key_authorization'

Vagrant.configure('2') do |config|
  config.vagrant.plugins = ["vagrant-hostsupdater", "vagrant-disksize"]
  config.vm.box = 'centos/8'
  config.disksize.size = '51GB'
  authorize_key_for_root config, '~/.ssh/id_dsa.pub', '~/.ssh/id_rsa.pub'

  {
    'vm1'   => '192.168.33.10',
    'vm2'   => '192.168.33.11',
  }.each do |short_name, ip|
    config.vm.define short_name do |host|
      host.vm.network 'private_network', ip: ip
      host.vm.hostname = "#{short_name}.code-challenge"
    end
  end
end
