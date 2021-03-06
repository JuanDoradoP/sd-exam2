VAGRANTFILE_API_VERSION = "2"

firstDisk = 'Disks/firstDisk.vdi'
secondDisk = 'Disks/secondDisk.vdi'
thirdDisk = 'Disks/thirdDisk.vdi'
fourthDisk = 'Disks/fourthDisk.vdi'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false
  config.vm.define :master do |master|
    master.vm.box = "centos/7"
    master.vm.network :private_network, ip: "192.168.50.10"
    master.vm.hostname = "master"
    master.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "2048","--cpus", "1", "--name", "master" ]
      unless File.exist?(firstDisk)
        vb.customize ['createhd', '--filename', firstDisk, '--variant', 'Fixed', '--size', 1024]
      end
      vb.customize ['storageattach', :id,  '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', firstDisk]
    end
  end

   config.vm.define :worker_1 do |n1|
     n1.vm.box = "centos/7"
     n1.vm.network :private_network, ip: "192.168.50.11"
     n1.vm.hostname = "nodo1"
     n1.vm.provider :virtualbox do |vb|
       vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "1", "--name", "worker_1" ]
       unless File.exist?(secondDisk)
         vb.customize ['createhd', '--filename', secondDisk, '--variant', 'Fixed', '--size', 1024]
       end
       vb.customize ['storageattach', :id,  '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', secondDisk]
     end
   end
 
   config.vm.define :worker_2 do |n2|
     n2.vm.box = "centos/7"
     n2.vm.network :private_network, ip: "192.168.50.12"
     n2.vm.hostname = "nodo2"
     n2.vm.provider :virtualbox do |vb|
       vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "1", "--name", "worker_2" ]
       unless File.exist?(thirdDisk)
         vb.customize ['createhd', '--filename', thirdDisk, '--variant', 'Fixed', '--size', 1024]
       end
       vb.customize ['storageattach', :id,  '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', thirdDisk]
     end
   end
 
   config.vm.define :worker_3 do |n3|
     n3.vm.box = "centos/7"
     n3.vm.network :private_network, ip: "192.168.50.13"
     n3.vm.hostname = "nodo3"
     n3.vm.provider :virtualbox do |vb|
       vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "1", "--name", "worker_3" ]
       unless File.exist?(fourthDisk)
         vb.customize ['createhd', '--filename', fourthDisk, '--variant', 'Fixed', '--size', 1024]
       end
       vb.customize ['storageattach', :id,  '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', fourthDisk]
     end
   end
  
   config.vm.provision "playbook1", type: "ansible" do |ansible|
     ansible.inventory_path = 'hosts'
     ansible.playbook = "dependencies_playbook.yml"
   end

   config.vm.provision "playbook2", type: "ansible" do |ansible|
     ansible.inventory_path = 'hosts'
     ansible.playbook = "swarm_playbook.yml"
   end

   config.vm.provision "playbook3", type: "ansible" do |ansible|
     ansible.inventory_path = 'hosts'
     ansible.playbook = "gluster_playbook.yml"
   end

   config.vm.provision "playbook4", type: "ansible" do |ansible|
     ansible.inventory_path = 'hosts'
     ansible.playbook = "files_playbook.yml"
   end

end
