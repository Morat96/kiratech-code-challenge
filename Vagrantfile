require_relative './scripts/key_authorization'

Vagrant.configure('2') do |config|
  config.vagrant.plugins = ["vagrant-hostsupdater", "vagrant-disksize", "vagrant-serverspec"]
  config.vm.box = 'centos/8'
  config.disksize.size = '51GB'
  authorize_key_for_root config, '~/.ssh/id_dsa.pub', '~/.ssh/id_rsa.pub'
  config.ssh.insert_key = false

  # How many vms are required
  N = 2
  (1..N).each do |host_id|
    config.vm.define "vm#{host_id}" do |host|
      host.vm.network 'private_network', ip: "192.168.33.1#{host_id}"
      host.vm.hostname = "vm#{host_id}.code-challenge"

      # Run after the second machine is up
      if host_id == N
        host.vm.provision "ansible" do |ansible|
          ansible.limit = 'all'
          ansible.inventory_path = 'hosts'
          ansible.playbook = 'playbook.yml'
        end
        host.vm.provision :serverspec do |spec|
          spec.pattern = 'scripts/*_spec.rb' # pattern for test files
        end
      end
    end
  end
end
