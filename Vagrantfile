# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.provision "shell", path: "script.sh"
  config.vm.provision "shell", inline: $script
end

$script = <<-SCRIPT
echo "########################################################"
echo "### Install Software ###################################"
echo "########################################################"
# Update the apt package index
apt-get update -y
  
# Install packages to allow apt to use a repository over HTTPS
sudo apt-get install -y \
	apt-transport-https \
	ca-certificates \
	curl \
    software-properties-common
  
echo "########################################################"
echo "### Install Docker #####################################"
echo "########################################################"
# Add Docker’s official GPG key:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  
# add the docker stable repository
sudo add-apt-repository \
	"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable"
  
apt-get update -y		
apt-get install -y docker-ce
  
echo "########################################################"
echo "### Install Docker Compose #############################"
echo "########################################################"
COMPOSE_VERSION=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d '"' -f4)
echo $COMPOSE_VERSION
curl -L "https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose 
docker-compose -v
SCRIPT