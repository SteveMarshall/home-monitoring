Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"
  config.vm.hostname = "monitoring"
  config.vm.provider "virtualbox" do |v|
    v.name = "monitoring"
    v.customize ["modifyvm", :id, "--nictype2", "virtio" ]
  end

  config.vm.network "public_network",
    bridge: "en0: Ethernet"

  config.vm.network "forwarded_port",
        guest: 3000, host: 3000
  config.vm.network "forwarded_port",
        guest: 9090, host: 9090
  config.vm.network "forwarded_port",
        guest: 9115, host: 9115
  # config.vm.network "forwarded_port",
  #       guest: 9798, host: 9798

  config.vm.provision :shell, inline: "apt-get update"
  config.vm.provision :docker
  config.vm.provision "shell", inline: <<-SHELL
    cd /vagrant
    docker compose stop
    docker compose up -d
  SHELL
end
