Vagrant.configure(2) do |config|
  config.vm.define "vmmaster" do |vmmaster|

 	vmmaster.vm.box = "ubuntu/bionic64"
 	vmmaster.vm.network "forwarded_port", guest: 9000, host: 9001
  	#vmmaster.vm.network "public_network", bridge: "ens3"
  	vmmaster.vm.network "private_network", ip: "192.168.50.10"
	vmmaster.vm.hostname = "vmmaster"
  	vmmaster.vm.provider "virtualbox" do |vb|
      		vb.memory = "4096"
    	  	vb.name = "vmmaster"
  	end
	vmmaster.vm.provision "shell", inline: <<-SHELL
		sudo apt update
		sudo apt -y upgrade
		wget -qO- https://get.docker.com/ | sh
		sudo apt update
		sudo apt -y install docker-ce docker-ce-cli containerd.io
		sudo systemctl start docker
		sudo systemctl enable docker
		sudo docker swarm init --advertise-addr 192.168.50.10:2377
		git clone https://github.com/RenatoAr/docker-appserver.git
		cd docker-appserver
		sudo docker build -t docker-appserver .
		sudo docker run -p 5000:5000 -it --name docker-appserver docker-appserver
	SHELL
  end
  config.vm.define "vmworker" do |vmworker|

 	vmworker.vm.box = "ubuntu/bionic64"
  	#vmworker.vm.network "public_network"
  	vmworker.vm.network "private_network", ip: "192.168.50.20"
	vmworker.vm.hostname = "vmworker"
  	vmworker.vm.provider "virtualbox" do |vb|
      		vb.memory = "2048"
    	  	vb.name = "vmworker"
  	end
	vmworker.vm.provision "shell", inline: <<-SHELL
		sudo apt update
		sudo apt -y upgrade
		wget -qO- https://get.docker.com/ | sh
		sudo apt update
		sudo apt -y install docker-ce docker-ce-cli containerd.io
		sudo systemctl start docker
		sudo systemctl enable docker
		git clone https://github.com/RenatoAr/docker-appclient.git
	SHELL
  end
end
