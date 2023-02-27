Vagrant.configure("2") do |config|
    
    config.vm.define "server1" do |server1|
        server1.vm.box = "rockylinux/9"
        server1.vm.hostname = "server1"
        server1.vm.network "private_network", ip: "192.168.33.51"
        server1.vm.provider "virtualbox" do |v|
            v.name = "server1"
            v.memory = 1024
            v.cpus = 1
        end
    end

    config.vm.define "server2" do |server2|
        server2.vm.box = "rockylinux/9"
        server2.vm.hostname = "server2"
        server2.vm.network "private_network", ip: "192.168.33.52"
        server2.vm.provider "virtualbox" do |v|
            v.name = "server2"
            v.memory = 1024
            v.cpus = 1
        end
    end

    config.vm.define "server3" do |server3|
        server3.vm.box = "rockylinux/9"
        server3.vm.hostname = "server3"
        server3.vm.network "private_network", ip: "192.168.33.53"
        server3.vm.provider "virtualbox" do |v|
            v.name = "server3"
            v.memory = 1024
            v.cpus = 1
        end
    end

    config.vm.define "workstation" do |workstation|
        workstation.vm.box = "rockylinux/9"
        workstation.vm.hostname = "workstation"
        workstation.vm.network "private_network", ip: "192.168.33.50"
        workstation.vm.provider "virtualbox" do |v|
            v.name = "workstation"
            v.memory = 1024
            v.cpus = 1
        end
  
        workstation.vm.provision "ansible_local" do |ansible|
          ansible.playbook = "setup.yml"
          ansible.install_mode = "default"
          ansible.verbose        = true
          ansible.limit          = "all"
          ansible.inventory_path = "inventory"
          ansible.config_file = "ansible.cfg"
          ansible.extra_vars = {
            ansible_connection: "ssh",
            ansible_user: "vagrant",
            ansible_ssh_pass: "vagrant",
          }
          #ansible.version = "2.2.1.0"
        end      
    end
  end
  