# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "hashicorp/precise32"

  # Port forwarding
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 6767, host: 6767

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Anything in ./mongrel-data will be mirrored to the guest
  config.vm.synced_folder "./mongrel-data", "/home/vagrant/mongrel-data"

  # VirtualBox settings
  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end

  # Very simple shell script ot download and install 0MQ and mongrel2
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get -qq -y update && apt-get -q -y install curl build-essential sqlite3 libsqlite3-dev uuid-dev
    sudo curl -L http://download.zeromq.org/zeromq-2.1.4.tar.gz | tar xz && cd zero* && ./configure && make && make install
    ldconfig -v
    cd /home/vagrant
    curl -L https://github.com/mongrel2/mongrel2/releases/download/1.9.2/mongrel2-v1.9.2.tar.bz2 | tar xj && cd mongrel* && make install
    cp examples/configs/sample.conf mysite.conf
    m2sh load -config mysite.conf
    mkdir run logs tmp
    chmod a+rwx logs
    m2sh start -host localhost
  SHELL
end
