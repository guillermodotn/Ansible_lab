Vagrant.configure("2") do |config|
    config.vm.box = "rockylinux/8"
    config.vm.network :private_network, ip: "192.168.33.10"
end

#Vagrant.configure("2") do |config|
#    config.vm.provision "shell", inline: "echo Hello"
#
#    servers=[
#        {
#            :hostname => "workstation",
#            :box => "rockylinux/8",
#            :ip => "172.16.1.50",
#        },
#        {
#            :hostname => "server1",
#            :box => "rockylinux/8",
#            :ip => "172.16.1.51",
#        },
#        {
#            :hostname => "server2",
#            :box => "rockylinux/8",
#            :ip => "172.16.1.52",
#        },
#        {
#            :hostname => "server3",
#            :box => "rockylinux/8",
#            :ip => "172.16.1.53",
#        },
#    ]
#
#    servers.each do |machine|
#        config.vm.define machine[:hostname] do |node|
#            node.vm.box = machine[:box]
#            node.vm.hostname = machine[:hostname]
#            node.vm.network = "private_network", ip: machine[:ip]
#        end
#    end
#end
  
