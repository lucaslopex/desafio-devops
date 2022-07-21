Vagrant.configure("2") do |config|
  config.vm.box = "gusztavvargadr/docker-linux"


config.vm.define "dockersrv" do |dockersrv|
  dockersrv.vm.network "public_network", bridge: "TP-Link Gigabit PCI Express Adapter", ip: "10.0.17.250"
  config.vm.network :forwarded_port, guest: 80, host: 80
  config.vm.network :forwarded_port, guest: 3000, host: 3000
  config.vm.network :forwarded_port, guest: 3306, host: 3306
  config.vm.network :forwarded_port, guest: 8080, host: 8080
end
end
