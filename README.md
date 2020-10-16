# Prerequesites 

# Vagrant

- Website: [https://www.vagrantup.com/](https://www.vagrantup.com/) -  Version 2.2.10
- Box: https://app.vagrantup.com/ubuntu/boxes/bionic64
- Virtual Machine: https://www.virtualbox.org/


## Quick Start

Build virtual environment:

    vagrant init ubuntu/bionic64
    vagrant up


### Note: 
- do loop is being set here as there are multiple tasks being set.
- gist is where the code is stored.
      
## Vagrantfile code:
-Configure vagrant file with the following below.

     config.vm.box = "ubuntu/bionic64"
     vagrant up config.vm.provision :shell do |shell|
     shell.name = "Provision Script 1"
     shell.privileged = "false"
     shell.args = ["arg1", "arg2", "arg3"]
     shell.path = "https://gist.githubusercontent.com/geoffreypf/6dd705d85dc8adae4eccee571e09542a/raw/88d1666cd22ca0c921205c6c9e819bbfa058a276/provision.sh"
     end
-Save the file and run the command vagrant up.
     
 ## Configuration for nginx loadbalancer and web servers
 -Configure vagrant file with the following below.
 
     config.vm.define "lb1" do |lb1|
     lb1.vm.box = "ubuntu/bionic64"
     lb1.vm.network "private_network", ip: "10.0.0.10"
     lb1.vm.provision "shell", path: "https://gist.githubusercontent.com/geoffreypf/7804b653c0c53ddab75b60fc9b69ff55/raw/3b53abd4d693a54c3d5837f5da6255f362233268/provision-lb.sh"
     end
    
     config.vm.define "web1" do |web1|
     web1.vm.box = "ubuntu/bionic64"
     web1.vm.network "private_network", ip: "10.0.0.11"
     web1.vm.provision :shell do |shell|
       shell.args = "1"
       shell.path = "https://gist.githubusercontent.com/geoffreypf/b791af32da7ebe9dac53a23bad0e91eb/raw/006478ece0320943d7b4c6fae9c74e0a4ea11d88/provision-web.sh"
      end
    end
    
      config.vm.define "web2" do |web2|
      web2.vm.box = "ubuntu/bionic64"
      web2.vm.network "private_network", ip: "10.0.0.12"
      web2.vm.provision :shell do |shell|
        shell.args = "2"
        shell.path = "https://gist.githubusercontent.com/geoffreypf/b791af32da7ebe9dac53a23bad0e91eb/raw/006478ece0320943d7b4c6fae9c74e0a4ea11d88/provision-web.sh"
     end
    end
-Save the file and run the command vagrant up.
