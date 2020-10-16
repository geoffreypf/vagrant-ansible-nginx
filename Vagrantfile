Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.define :loadbalancer do |loadbalancer|
        loadbalancer.vm.provider :virtualbox do |v|
            v.name = "loadbalancer"
            v.customize [
                "modifyvm", :id,
                "--name", "loadbalancer",
                "--memory", 512,
                "--natdnshostresolver1", "on",
                "--cpus", 1,
            ]
        end

        loadbalancer.vm.box = "ubuntu/bionic64"
        loadbalancer.vm.network :private_network, ip: "192.168.30.10"
        loadbalancer.ssh.forward_agent = true
        loadbalancer.vm.synced_folder "./", "/vagrant", :nfs => true
    end

  config.ssh.insert_key = false
  config.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa']
  config.vm.provision "file", source: "keys/.ssh/vagrant_rsa.pub", destination: "~/.ssh/authorized_keys"
  
  config.vm.network "forwarded_port", guest: 80, host: 8085
  ####### Provision #######
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provision/playbook.yml"
    ansible.verbose = true
  end
end