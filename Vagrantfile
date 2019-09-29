# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # Use Ubuntu 14.04 Trusty Tahr 64-bit as our operating system
  config.vm.box = "ubuntu/trusty64"

  # Configurate the virtual machine to use 2GB of RAM
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--name", "Ansible Dev VM"]
  end

  # Forward the Rails server default port to the host
  config.vm.network :forwarded_port, guest: 3000, host: 3000

  # Forward http and https ports
  config.vm.network :forwarded_port, guest: 80, host: 80
  config.vm.network :forwarded_port, guest: 443, host: 443

  # postgresql
  config.vm.network :forwarded_port, guest: 5432, host: 5432
  # mongodb
  config.vm.network :forwarded_port, guest: 27017, host: 27017
  config.vm.network :forwarded_port, guest: 28017, host: 28017
  # redis
  config.vm.network :forwarded_port, guest: 6379, host: 6379
  # rabbitmq
  config.vm.network :forwarded_port, guest: 5672, host: 5672
  config.vm.network :forwarded_port, guest: 15671, host: 15671
  config.vm.network :forwarded_port, guest: 25672, host: 25672

  # synced folders
  config.vm.synced_folder "workspace/", "/vagrant/workspace"

  # ansible provisioning
  config.vm.provision :ansible_local do |ansible|
    ansible.become = true
    ansible.playbook = 'provisioning/main.yml'
  end

end
