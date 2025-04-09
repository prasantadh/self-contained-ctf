# Vagrant file to get a kali machine up along with some ubuntu machines 
# Kali NUMBER_OF_SESSIONS VNC sessions available over PORT 8001 onwards 
# NUMBER_OF_TEAMS ubuntu machines are spawned
Vagrant.configure(2) do |config| 

  number_of_teams = ENV.fetch("NUMBER_OF_TEAMS", 1).to_i
  number_of_sessions = ENV.fetch("NUMBER_OF_SESSIONS", 3).to_i


  # Spin up the Kali Virtual Machine with ansible to start the VNC sessions
  config.vm.define "kali" do |kali|
    kali.vm.box = "kalilinux/rolling"

    kali.vm.network "private_network", ip: "192.168.56.2"

    kali.vm.provider "virtualbox" do |vb|
      vb.memory = "6144"
      vb.gui = false
      vb.cpus = 6
    end

    kali.vm.provision :ansible do |ansible| 
      ansible.playbook = "provisioning/kali_setup.yaml"
      ansible.extra_vars = {
        number_of_sessions: number_of_sessions
      }
    end
  end

  (1..number_of_teams).each do |team|

    config.vm.define "ubuntu-#{team}" do |ubuntu|
      ubuntu.vm.box = "bento/ubuntu-24.04"

      ubuntu.vm.network "private_network", ip: "192.168.56.#{200 + team}"

      ubuntu.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.gui = false
        vb.cpus = 2
      end
    end

  end

end
