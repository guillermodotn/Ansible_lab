SERVERS = {
  "server1" => { ip: "192.168.33.51", box: "generic/centos10s" },
  "server2" => { ip: "192.168.33.52", box: "generic/centos10s" },
  "server3" => { ip: "192.168.33.53", box: "generic/centos10s" },
  "server4" => { ip: "192.168.33.54", box: "bento/ubuntu-26.04" },
}

Vagrant.configure("2") do |config|
  config.vm.synced_folder ".", "/vagrant", type: "rsync",
    rsync__exclude: [".git/", ".vagrant/"]

  config.vm.provider "libvirt" do |lv|
    lv.driver = "kvm"
    lv.memory = 1024
    lv.cpus = 1
  end

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 1
    vb.linked_clone = true
  end

  config.vm.provider "vmware_desktop" do |vmw|
    vmw.vmx["memsize"] = "1024"
    vmw.vmx["numvcpus"] = "1"
  end

  SERVERS.each do |name, opts|
    config.vm.define name do |node|
      node.vm.box = opts[:box]
      node.vm.hostname = name
      node.vm.network "private_network", ip: opts[:ip]
    end
  end

  config.vm.define "workstation", primary: true do |workstation|
    workstation.vm.box = "generic/fedora44"
    workstation.vm.hostname = "workstation"
    workstation.vm.network "private_network", ip: "192.168.33.50"

    workstation.vm.provider "libvirt" do |lv|
      lv.memory = 2048
      lv.cpus = 2
    end

    workstation.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    workstation.vm.provider "vmware_desktop" do |vmw|
      vmw.vmx["memsize"] = "2048"
      vmw.vmx["numvcpus"] = "2"
    end

    workstation.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "setup.yml"
      ansible.install_mode = "default"
      ansible.verbose = true
      ansible.limit = "all"
      ansible.inventory_path = "inventory"
      ansible.config_file = "ansible.cfg"
      ansible.extra_vars = {
        ansible_connection: "ssh",
        ansible_user: "vagrant",
        ansible_ssh_pass: "vagrant",
      }
    end
  end
end
