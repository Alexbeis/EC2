Vagrant.require_version ">= 1.5"
 
 Vagrant.configure("2") do |config|
 
     config.vm.box     = "nrel/CentOS-6.7-x86_64"
     config.ssh.forward_agent = true
 
     config.vm.synced_folder "../ansible", "/ansible"
     #config.vm.synced_folder "myshared", "/home/vagrant/myshared", owner: "vagrant", group: "vagrant", create: true
  
    config.ssh.insert_key = "false"
 
     config.vm.provider "virtualbox" do |v|
         v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
         v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
     end
 
     config.vm.define "web", primary: true do |web|
       	web.vm.network :private_network, ip: "192.168.33.50"
       	web.vm.network :forwarded_port, guest: 80, host: 8080, auto_correct: true
      	web.vm.network :forwarded_port, guest: 443, host: 8081, auto_correct: true
 
      	web.vm.hostname = "ansibleMpwar"
        web.vm.provision :shell, path: "shell/vagrant_main_provision.sh"


     end
 end