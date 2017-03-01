# -*- mode: ruby -*-
#

##### Don't change code below! ######

$install_utils_script = <<SCRIPT
echo Installing utils...
sh -c "echo \"LANG=en_US.UTF-8\" >> /etc/environment"
sh -c "echo \"LANGUAGE=en_US.UTF-8\" >> /etc/environment"
sh -c "echo \"LC_ALL=en_US.UTF-8\" >> /etc/environment"
sh -c "echo \"LC_CTYPE=en_US.UTF-8\" >> /etc/environment"
source /etc/environment
apt-get update     
apt-get install -y wget mc unzip git
SCRIPT

$install_docker_script = <<SCRIPT
echo Installing Docker...
export DEBIAN_FRONTEND=noninteractive
#echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections
curl -sSL https://get.docker.com/ | sh
usermod -aG docker vagrant
sh -c "curl -L https://github.com/docker/compose/releases/download/1.11.2/run.sh > /usr/local/bin/docker-compose"
chmod +x /usr/local/bin/docker-compose
SCRIPT

$install_jdk_script = <<SCRIPT
echo Installing Open-JDK-8...
add-apt-repository ppa:openjdk-r/ppa -y
apt-get update
apt-get install openjdk-8-jdk -y
sh -c "echo \"JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64\" >> /etc/environment"
source /etc/environment
java -version
echo $JAVA_HOME
SCRIPT


Vagrant.configure(2) do |config|
  config.vm.box = 'ubuntu/trusty64'
  config.vm.box_check_update = false
  config.vm.provision "shell", inline: $install_utils_script, privileged: true
  config.vm.provision "shell", inline: $install_docker_script, privileged: true
end

