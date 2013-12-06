Vagrant.configure("2") do |config|
  config.vm.box = "centos64-lamp"
  config.vm.box_url = "http://box.puphpet.com/centos64-x64-vbox43.box"

  config.vm.network "private_network", ip: "192.168.56.111"

  config.vm.network "forwarded_port", guest: 8080, host: 80

  config.vm.synced_folder "/Users/kadir/Projects/webs/", "/var/www", id: "vagrant-root", :nfs => false
  config.vm.synced_folder "/Users/kadir/Projects/mysqlDataDir/centos64-lamp/", "/var/vagrantmysql",:mount_options => ["uid=27", "gid=27"]
  config.vm.usable_port_range = (2200..2250)
  config.vm.provider :virtualbox do |virtualbox|
    virtualbox.customize ["modifyvm", :id, "--name", "centos64-lamp"]
    virtualbox.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    virtualbox.customize ["modifyvm", :id, "--memory", "1048"]
    virtualbox.customize ["setextradata", :id, "--VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end

  config.vm.provision :shell, :path => "shell/initial-setup.sh"
  config.vm.provision :shell, :path => "shell/update-puppet.sh"
  config.vm.provision :shell, :path => "shell/librarian-puppet-vagrant.sh"
  config.vm.provision :puppet do |puppet|
    puppet.facter = {
      "ssh_username" => "vagrant"
    }

    puppet.manifests_path = "puppet/manifests"
    puppet.options = ["--verbose", "--hiera_config /vagrant/hiera.yaml", "--parser future"]
  end
  config.ssh.username = "vagrant"

  config.ssh.shell = "bash -l"

  config.ssh.keep_alive = true
  config.ssh.forward_agent = false
  config.ssh.forward_x11 = false
  config.vagrant.host = :detect
end

