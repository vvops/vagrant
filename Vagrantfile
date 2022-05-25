Vagrant.configure("2") do |config|
	(61..65).each do |i|
		config.vm.define "server#{i}" do |web|
			web.vm.box = "ubuntu/focal64"			
			web.vm.network "public_network", ip: "192.168.1.#{i}", netmask: "24"
			web.vm.hostname = "server#{i}"

			web.vm.provision "shell" do |s|
				ssh_pub_key = File.readlines("C:/Users/vovas/.ssh/ansible/id_rsa.pub").first.strip
				s.inline = <<-SHELL
				echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
				echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
				SHELL
			end
			

			web.vm.provider "virtualbox" do |v|
				v.name = "server#{i}"
				v.memory = 1500
				v.cpus = 1
			end
		end
	end
end