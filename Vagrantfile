
Vagrant.configure(2) do |config|
  config.vm.box = "debian/jessie64"
  config.vm.box_check_update = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "consul" do |consul|
    consul.vm.hostname = "consul"
    consul.vm.network "private_network", ip: "192.168.99.99"

    consul.vm.provider "virtualbox" do |virtualbox|
      virtualbox.customize [ "guestproperty", "set", :id,
                             "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold",
                             10000 ]
      virtualbox.memory = 512
      virtualbox.cpus = 1
    end

    consul.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/consul.yml"
    end
  end

  config.vm.define "graylog" do |graylog|
    graylog.vm.hostname = "graylog"
    graylog.vm.network "private_network", ip: "192.168.99.2"

    graylog.vm.provider "virtualbox" do |virtualbox|
      virtualbox.memory = 4096
      virtualbox.cpus = 2
      virtualbox.customize [ "guestproperty", "set", :id,
                             "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold",
                             10000 ]
    end

    graylog.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/graylog.yml"
    end
  end

  config.vm.define "kafka" do |kafka|
    kafka.vm.hostname = "kafka"
    kafka.vm.network "private_network", ip: "192.168.99.3"

    kafka.vm.provider "virtualbox" do |virtualbox|
      virtualbox.memory = 2048
      virtualbox.cpus = 1
      virtualbox.customize [ "guestproperty", "set", :id,
                             "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold",
                             10000 ]
    end

    kafka.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/kafka.yml"
    end
  end

  config.vm.define "prometheus" do |prometheus|
    prometheus.vm.hostname = "prometheus"
    prometheus.vm.network "private_network", ip: "192.168.99.4"

    prometheus.vm.provider "virtualbox" do |virtualbox|
      virtualbox.customize [ "guestproperty", "set", :id,
                             "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold",
                             10000 ]
      virtualbox.memory = 512
      virtualbox.cpus = 1
    end

    prometheus.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/prometheus.yml"
    end
  end
end
