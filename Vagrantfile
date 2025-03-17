Vagrant.configure(2) do |config| 

  number_of_teams = ENV.fetch("NUMBER_OF_TEAMS", 1).to_i

  (1..number_of_teams).each do |team|

    # Spin up the Kali Virtual Machines
    config.vm.define "kali-#{team}" do |kali|
      kali.vm.box = "kalilinux/rolling"
  
      kali.vm.network "private_network", ip: "192.168.56.#{team + 1}"

      kali.vm.provider "virtualbox" do |vb|
        vb.memory = "6144"
        vb.gui = false
        vb.cpus = 6
      end

      kali.vm.provision :ansible do |ansible| 
        ansible.playbook = "provisioning/kali_setup.yaml"
      end
    end

    config.vm.define "ubuntu-#{team}" do |ubuntu|
      ubuntu.vm.box = "bento/ubuntu-24.04"

      ubuntu.vm.network "private_network", ip: "192.168.56.#{team * 100 + 1}"

      ubuntu.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.gui = false
        vb.cpus = 2
      end
    end

  end

end
