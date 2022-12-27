def install_plugin(plugin)
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

# 必要なプラグインを指定
install_plugin('vagrant-vbguest')
install_plugin('vagrant-cachier')
install_plugin('vagrant-timezone')
install_plugin('vagrant-docker-compose')
install_plugin('dotenv')

Dotenv.load('.env.local', '.env')
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/jammy64"
  config.vm.box_version = "20221219.0.0"
  config.vm.boot_timeout = ENV['VM_BOOT_TIMEOUT'].to_i

  config.timezone.value = "Asia/Tokyo"
  config.cache.scope = :box

  config.vm.synced_folder "./docker", "/vagrant/docker"
  config.vm.provision :docker
  config.vm.provision :docker_compose,
    yml: [
      "/vagrant/docker/docker-compose.yml",
      "/vagrant/docker/docker-compose.override.yml"
    ],
    options: " --project-directory /vagrant/docker",
    run: "always"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  config.vm.define "forward-port" do |machine|
    machine.vm.network "forwarded_port", guest: 8000, host: 50000
    machine.vm.network "forwarded_port", guest: 8001, host: 50001
  end

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.define "private-net" do |machine|
    machine.vm.network "private_network", ip: "192.168.33.11"
  end

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true

    # Customize the amount of memory on the VM:
    vb.cpus = ENV['VIRTUALBOX_CPUS']
    vb.memory = ENV['VIRTUALBOX_MEMORY']
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
