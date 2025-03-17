Vagrant.configure(2) do |config| 
  config.vm.box = "kalilinux/rolling"
  
  config.vm.network "private_network", ip: "192.168.56.2"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "6144"
    vb.gui = false
    vb.cpus = 6
  end

  config.vm.provision :ansible do |ansible| 
    ansible.playbook = "provisioning/kali_setup.yaml"
  end

end
