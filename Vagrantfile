
Vagrant.configure(2) do |config|
  config.vm.box = "debian/jessie64"
  config.vm.hostname = "graylog"
  config.vm.provider "virtualbox" do |virtualbox|
    virtualbox.memory = 4096
    virtualbox.cpus = 2
  end
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provisioning/graylog.yml"
  end
  config.vm.network "private_network", ip: "192.168.99.2"
  config.vm.network "forwarded_port", guest: 80, host: 9000
end
