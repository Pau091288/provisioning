$script = <<SCRIPT
vagrant plugin install vagrant-hostmanager
vagrant plugin install vagrant-vbguest
SCRIPT

hosts = {
  "test01"   => { ip: "192.168.50.10", port: 2201 },
  "test02"   => { ip: "192.168.50.11", port: 2202 }, 
}

Vagrant.configure("2") do |config|
  hosts.each do |name, host_config|
    config.vm.define name do |machine|
      #machine.vm.box = "ubuntu/xenial64"
      machine.vm.box = "ubuntu/xenial64"
      machine.vm.network :private_network, ip: host_config[:ip]

      machine.vm.provider "virtualbox" do |v|
          v.name = name
          v.customize ["modifyvm", :id, "--memory", 2024]
      end

      machine.vm.provision "ansible" do |ansible|
          ansible.verbose = true
          ansible.playbook = "playbooks/common.yml"
      end
    end
    config.vm.network :forwarded_port, guest: 22, host: host_config[:port], id: "ssh", auto_correct: true

  end
end
