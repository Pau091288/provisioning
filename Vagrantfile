hosts = {
  "test01"   => { ip: "192.168.50.10", port: 2201 },
  "test02"   => { ip: "192.168.50.11", port: 2202 }, 
}

Vagrant.configure("2") do |config|
  hosts.each do |name, host_config|
    config.vm.define name do |machine|
    	machine.vm.box = "ubuntu/xenial64"
    end
  end
end
