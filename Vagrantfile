Vagrant.configure("2") do |config|

  forward_port = ->(guest, host = guest) do
    config.vm.network :forwarded_port,
      guest: guest,
      host: host,
      auto_correct: true
  end

  config.vm.box = "hashicorp/precise64"
  # Sync between the web root of the VM and the 'sites' directory
  config.vm.synced_folder "sites/", "/srv/www", :owner=> 'root', :group=>'root', :mount_options => ['dmode=775', 'fmode=775']
  forward_port[1080]      # mailcatcher
  forward_port[3306]      # mysql
  forward_port[80, 8080]  # nginx/apache

  config.vm.provision "chef_solo" do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.data_bags_path = "data_bags"
    chef.add_recipe "apt"
    chef.add_recipe "mautic"
  end

end
