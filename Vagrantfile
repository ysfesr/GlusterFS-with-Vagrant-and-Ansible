Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox"
  config.vm.box = "centos/7"
  config.vm.box_check_update = false
  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.cpus = 2
    vb.memory = "2048"
  end
 
  N = 3
  (1..N).each do |machine_id|
    config.vm.define "node#{machine_id}" do |machine|
      machine.vm.hostname = "node#{machine_id}"
      machine.vm.network "private_network", ip: "192.168.56.#{10+machine_id}"
  

      if machine_id == N
        machine.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.playbook = "playbook.yml"
          ansible.inventory_path = "hosts"
          ansible.verbose = false
          ansible.become = true
        end
      end
    end
  end

end