# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.hostname = "vagrant.pfe"
  config.vm.box = "ubuntu/precise64"
  config.vm.provision :shell, :path => "./provisioning/bin/vagrant-install.sh"
  config.vm.provision :shell, :path => "./provisioning/bin/vagrant-config.sh"

  config.vm.network "private_network", ip: "10.0.1.10"
  config.vm.network "forwarded_port", guest: 80, host: 80
  config.vm.network "forwarded_port", guest: 3306, host: 3306

  # stdin: is not a tty => https://github.com/mitchellh/vagrant/issues/1673
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

  config.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
  end

  # Config synced folder
  if Vagrant::Util::Platform.windows?
    config.vm.synced_folder ".", "/files"
  else
    config.vm.synced_folder ".", "/files"
    # config.vm.synced_folder ".", "/files", type: "nfs"
  end
end
