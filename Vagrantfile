# -*- mode: ruby -*-
# vi: set ft=ruby :

ica_client_version = "26.01.0.150"
ica_client_version_sha256 = "7ce8c3a32e1e9d698e7bca349ad582136040774a49e35f47e529430918f8b94a"
ica_client_file = "icaclient_#{ica_client_version}_amd64.deb"
sha256 = Digest::SHA256.file File.join File.dirname(__FILE__), ica_client_file
raise "SHA256 mismatch" unless sha256.hexdigest == ica_client_version_sha256.downcase

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # https://app.vagrantup.com/ubuntu
  config.vm.box = "ubuntu/jammy64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = true

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  config.ssh.forward_x11 = true

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
    vb.gui = false

    # Customize the amount of memory on the VM:
    vb.memory = "4096"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get upgrade
    apt-get install -y \
desktop-file-utils \
firefox \
net-tools \
xdg-utils \

  SHELL
  config.vm.provision "shell", inline: <<-SHELL
  # Snap changes the $HOME path, so the fallback file ~/.Xauthority does not exists inside snap, so we must set XAUTHORITY.
echo 'export XAUTHORITY=$HOME/.Xauthority' >> /home/vagrant/.profile
  SHELL
  config.vm.provision "file", source: ica_client_file, destination: ica_client_file
  config.vm.provision "shell", inline: <<-SHELL
    DEBIAN_FRONTEND=noninteractive apt-get install -y ./#{ica_client_file}
  SHELL
end
