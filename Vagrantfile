Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"
  config.vm.hostname = "monitoring"

  config.vm.network "public_network",
    bridge: "en0: Ethernet"
  config.vm.provider "vmware_desktop" do |vmware|
    vmware.vmx["ethernet0.virtualDev"] = "vmxnet3"
  end


  config.vm.synced_folder ".", "/vagrant", type: "nfs",
    nfs_udp: false
  # Required for nfs folder sharing
  config.vm.network "private_network", type: "dhcp"

  config.vm.provision :docker
  config.vm.provision "shell", inline: <<-SHELL
    cd /vagrant
    docker compose stop
    docker compose up -d --pull always
  SHELL
end
