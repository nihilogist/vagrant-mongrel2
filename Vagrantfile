# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  config.vm.box = "hashicorp/precise32"

  # Port forwarding
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 6767, host: 6767

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "/data", "/mongrel_data"

  # VirtualBox settings
  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end
  

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get -qq -y update && apt-get -q -y install curl build-essential sqlite3 libsqlite3-dev uuid-dev
    sudo curl -L http://download.zeromq.org/zeromq-2.1.4.tar.gz | tar xz && cd zero* && ./configure && make && make install
    ldconfig -v
    cd
    sudo curl -L https://github.com/mongrel2/mongrel2/releases/download/1.9.2/mongrel2-v1.9.2.tar.bz2 | tar xj && cd mongrel* && make install
  SHELL
end
