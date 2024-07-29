# -*- mode: ruby -*-
# vi: set ft=ruby :

ica_client_version = "24.5.0.76"
ica_client_version_sha256 = "c4b078199cf720dde618a2b3a56250cd3c32d12262b1973d4e04ee8ddf1837b8"
ica_client_file = "icaclient_#{ica_client_version}_amd64.deb"
sha256 = Digest::SHA256.file File.join File.dirname(__FILE__), ica_client_file
raise "SHA256 mismatch" unless sha256.hexdigest == ica_client_version_sha256.downcase

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2204"
  config.vm.box_check_update = true

  config.ssh.forward_x11 = true

  config.vm.provision "file", source: ica_client_file, destination: ica_client_file
  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    apt-get update
    apt-get upgrade
    add-apt-repository -y ppa:mozillateam/ppa
    apt-get install -y xauth xorg xdg-utils firefox-esr
    apt install -f ./#{ica_client_file} -y

    if [ ! -L /usr/bin/firefox ]; then ln -s /usr/bin/firefox-esr /usr/bin/firefox; fi
    sed -i 's/^#X11UseLocalhost yes/X11UseLocalhost no/' /etc/ssh/sshd_config && systemctl restart sshd
  SHELL
end
