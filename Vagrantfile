box_name = "opscode_ubuntu-12.04_chef-11.2.0"
box_url  = "https://opscode-vm.s3.amazonaws.com/vagrant/#{box_name}.box"
api_version = "2"

Vagrant.configure(api_version) do |config|
  config.vm.box               = box_name
  config.vm.box_url           = box_url
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.verbose = true
    ansible.sudo = true
    ansible.extra_vars = {
      gocd: {
        agent: { 
          instances: 2
        },
        server: {
          host: "127.0.0.1",
          port: 8153,
          autoregister_key: "this-is-insecure"
        }
      }
  }
  end
  config.vm.network "forwarded_port", guest: 8153, host: 8155
  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--memory", "1024"]
  end
end
