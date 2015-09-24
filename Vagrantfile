Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.provision "chef_solo" do |chef|
    chef.add_recipe "apt"
    chef.add_recipe "mautic"
    chef.data_bags_path = "data_bags"
  end
  config.vm.network "forwarded_port", guest: 80, guest_ip: "10.0.2.15", host: 8080
end
