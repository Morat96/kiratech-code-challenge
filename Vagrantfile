Vagrant.configure('2') do |config|
  config.vagrant.plugins = ["vagrant-hostsupdater", "vagrant-disksize"]
  config.vm.box = 'centos/7'
  config.disksize.size = '50GB'
  config.vm.provision "shell" do |s|
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        mkdir -p /root/.ssh/
        touch /root/.ssh/authorized_keys
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
      SHELL
    end

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
