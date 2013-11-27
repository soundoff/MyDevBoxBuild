Vagrant.configure("2") do |config|
    config.vm.box = "centos64_x86_64"
    config.vm.box_url = "http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-x86_64-v20130731.box"
    config.vm.hostname = "devbox"
    config.vm.network "forwarded_port", guest: 80, host: 8080
    config.vm.network "private_network", ip: "192.168.50.4"

    config.vm.provider :virtualbox do |virtualbox|
        virtualbox.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        virtualbox.customize ["modifyvm", :id, "--memory", "1024"]
    end

    config.vm.provision :shell, :path => "shell/initial-setup.sh"

    config.vm.provision :puppet do |puppet|
        puppet.manifests_path = "puppet/manifests"
        puppet.manifest_file = "default.pp"
    end

    config.vm.synced_folder "/projects", "/home/projects"
end
