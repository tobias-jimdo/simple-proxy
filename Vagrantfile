Vagrant.configure(2) do |config|
  config.vm.box = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  config.vm.network "public_network"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/node.yml"
    ansible.extra_vars = "ansible_extra_vars.yml"
  end
end
