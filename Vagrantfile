# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

#https://docs.docker.com/engine/install/debian/
$debian_bullseye_docker_script = <<-SCRIPT

#Unable to locate package docker-engine
#apt-get remove docker docker-engine docker.io containerd runc


# Set up the repository
apt-get update -y
apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y

#Add Docker’s official GPG key
mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# set up the repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null



#Install Docker Engine
apt-get update -y

apt-get install \
  docker-ce \
  docker-ce-cli \
  containerd.io \
  docker-compose-plugin -y


docker --version

# Verify that Docker Engine is installed correctly
docker run hello-world

# Post-installation steps for Linux
# Manage Docker as a non-root user

# Create the docker group
groupadd docker
# Add your user to the docker group
# usermod -aG docker $USER # by default run by root
usermod -aG docker vagrant

SCRIPT



$centos_stream_docker_script = <<-SCRIPT
# https://docs.docker.com/engine/install/centos/

# Uninstall old versions
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine

# # Set up the repository
yum install -y yum-utils
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo


# # Install Docker Engine
yum update -y
yum install \
    docker-ce \
    docker-ce-cli \
    containerd.io -y

#Start Docker
systemctl start docker

#Verify that Docker Engine is installed correctly
docker run hello-world

#Uninstall Docker Engine
# yum remove docker-ce docker-ce-cli containerd.io -y
# Images, containers, volumes, or customized configuration files on your host are not automatically removed.
# delete all images, containers, and volumes
# rm -rf /var/lib/docker
# rm -rf /var/lib/containerd

# https://docs.docker.com/engine/install/linux-postinstall/
# Post-installation steps for Linux

# Manage Docker as a non-root user
# Create the docker group
# groupadd docker #groupadd: group 'docker' already exists

# Add your user to the docker group
# usermod -aG docker $USER # by default run by current user root
usermod -aG docker vagrant

# newgrp docker #activate the changes to groups
su -c  'newgrp docker' vagrant

# Verify that you can run docker commands without sudo
# docker run hello-world
su -c  'docker run hello-world' vagrant #run by vagrant user


# Configure Docker to start on boot
systemctl enable docker.service
systemctl enable containerd.service


SCRIPT

$rsyslog_debian_script = <<-SCRIPT

apt-get update -y 
apt-get install rsyslog -y
rsyslogd -v

echo "backup /etc/rsyslog.conf.."
cp /etc/rsyslog.conf{,.orig}

echo "uncomment udp/tcp settings..."
sleep 5

echo "comment out below line"
grep 'module(load="imudp")' /etc/rsyslog.conf
sed -i '/module(load="imudp")/s/^#//g' /etc/rsyslog.conf #to uncomment
echo "verifying.."
grep 'module(load="imudp")' /etc/rsyslog.conf #verify

echo "uncomment udp/tcp settings..."
sleep 5


grep 'input(type="imudp" port="514")' /etc/rsyslog.conf
sed -i '/input(type="imudp" port="514")/s/^#//g' /etc/rsyslog.conf #to uncomment
echo "verifying.."
grep 'input(type="imudp" port="514")' /etc/rsyslog.conf


echo "uncomment udp/tcp settings..."
sleep 5


grep '#module(load="imtcp")' /etc/rsyslog.conf
sed -i '/#module(load="imtcp")/s/^#//g' /etc/rsyslog.conf #to uncomment
echo "verifying.."
grep 'module(load="imtcp")' /etc/rsyslog.conf

echo "uncomment udp/tcp settings..."
sleep 5

grep '#input(type="imtcp" port="514")' /etc/rsyslog.conf
sed -i '/#input(type="imtcp" port="514")/s/^#//g' /etc/rsyslog.conf #to uncomment
echo "verifying.."
grep 'input(type="imtcp" port="514")' /etc/rsyslog.conf

echo "replace tcp 514 port with 1468"
sleep 5

grep 'input(type="imtcp" port="514")' /etc/rsyslog.conf
sed -i.bck 's/nput(type="imtcp" port="514")/nput(type="imtcp" port="1468")/' /etc/rsyslog.conf
grep 'input(type="imtcp" port="1468")' /etc/rsyslog.conf

echo "restart rsyslog service"

echo "Check Rsyslog Configuration for Errors"
rsyslogd -f /etc/rsyslog.conf -N1 

systemctl restart rsyslog.service
systemctl enable rsyslog.service

echo "Listening on TCP 1468"
ss -tulnp | grep 1468

tail -f /var/log/messages

SCRIPT

$rsyslog_centos_stream8_script = <<-SCRIPT

yum update -y
yum install rsyslog -y

echo "backup /etc/rsyslog.conf.."
cp /etc/rsyslog.conf{,.orig}

echo "Enable sending system logs over UDP to rsyslog server"
echo "Enable sending system logs over TCP to rsyslog server"

cat <<EOT | sudo tee -a /etc/rsyslog.conf
#Enable sending system logs over UDP to rsyslog server
*.*  @192.168.50.6:514

#Enable sending system logs over TCP to rsyslog server
*.*  @@192.168.50.68:1468
EOT

cat /etc/rsyslog.conf

echo "Check Rsyslog Configuration for Errors"
rsyslogd -f /etc/rsyslog.conf -N1 

systemctl restart rsyslog.service
systemctl enable rsyslog.service

echo "Sending log."
logger "Test message from the system `hostname`" 

SCRIPT

$syslogng_01_debian_script = <<-SCRIPT

apt-get update -y 
apt-get install  syslog-ng -y

echo "backup /etc/syslog-ng/syslog-ng.conf .."
mv /etc/syslog-ng/syslog-ng.conf{,.orig}


echo "create /etc/syslog-ng/syslog-ng.conf"

cat <<EOT | sudo tee /etc/syslog-ng/syslog-ng.conf

@version: 3.5
@include "scl.conf"
@include "`scl-root`/system/tty10.conf"
options {
time-reap(30);
mark-freq(10);
keep-hostname(yes);
};
source s_local { system(); internal(); };
source s_network {
syslog(transport(tcp) port(514));
};
destination d_local {
file("/var/log/syslog-ng/messages_${HOST}"); };
destination d_logs {
file(
"/var/log/syslog-ng/logs.txt"
owner("root")
group("root")
perm(0777)
); };
log { source(s_local); source(s_network); destination(d_logs); };

EOT

cat /etc/syslog-ng/syslog-ng.conf

echo "create log dir"

mkdir -p /var/log/syslog-ng 
touch /var/log/syslog-ng/logs.txt

echo "Start and enable syslog-ng"

systemctl start syslog-ng
systemctl enable syslog-ng

echo "View the log files"

echo "Listening ports"
netstat -tanpu|grep syslog

tail -f /var/log/syslog-ng/logs.txt

SCRIPT

$syslogng_02_debian_script = <<-SCRIPT

apt-get update -y 
apt-get install  syslog-ng -y

echo "backup /etc/syslog-ng/syslog-ng.conf .."
mv /etc/syslog-ng/syslog-ng.conf{,.orig}


echo "create /etc/syslog-ng/syslog-ng.conf"

cat <<EOT | sudo tee /etc/syslog-ng/syslog-ng.conf
@version: 3.5
@include "scl.conf"
@include "`scl-root`/system/tty10.conf"
source s_local { system(); internal(); };
destination d_syslog_tcp {
syslog("192.168.50.8" transport("tcp") port(514)); };
log { source(s_local);destination(d_syslog_tcp); };
EOT

cat /etc/syslog-ng/syslog-ng.conf


echo "Start and enable syslog-ng"

systemctl start syslog-ng
systemctl enable syslog-ng

SCRIPT


Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |vb|
    # vb.gui = false
    vb.memory = "1024"
    vb.cpus = 2
    # vb.customize ["modifyvm", :id, "--groups", "/kali-sandbox"] # create vbox group
  end




        config.vm.define "vg-rsyslog-01" do |kalicluster|
          # https://app.vagrantup.com/debian/boxes/bullseye64
          # kalicluster.vm.box = "debian/bullseye64" #debian 11
          # https://github.com/chef/bento/tree/main/packer_templates/debian
          kalicluster.vm.box = "bento/debian-10.11" #debian 11
          kalicluster.vm.hostname = "vg-rsyslog-01"
          # kalicluster.vm.network "public_network"
          kalicluster.vm.network "private_network", ip: "192.168.50.6"
          # kalicluster.vm.network "forwarded_port", guest: 80, host: 81
          #Disabling the default /vagrant share can be done as follows:
          # kalicluster.vm.synced_folder ".", "/vagrant", disabled: true
          kalicluster.vm.provider "virtualbox" do |vb|
              vb.name = "vbox-rsyslog-01"
              vb.memory = "768"
              vb.gui = false
          end
          # kalicluster.vm.provision "shell", inline: $debian_bullseye_docker_script          
          kalicluster.vm.provision "shell", inline: $rsyslog_debian_script
          # kalicluster.vm.provision :shell, path: "provisioning/bootstrap.sh"

        end

        config.vm.define "vg-rsyslog-02" do |kalicluster|
          # https://app.vagrantup.com/centos/boxes/8
          # kalicluster.vm.box = "centos/8"  #NOT OK
          # https://github.com/chef/bento/blob/main/packer_templates/centos/centos-stream-8-x86_64.json
          kalicluster.vm.box = "bento/centos-stream-8"
          # https://app.vagrantup.com/centos/boxes/stream8
          # kalicluster.vm.box = "centos/stream8"
          kalicluster.vm.hostname = "vg-rsyslog-02"
          #bridged network,DHCP enabled,auto IP assignment
          kalicluster.vm.network "public_network" #NOT OK
          #bridged network,DHCP disabled, manual IP assignment
          # kalicluster.vm.network "public_network", ip: "10.35.8.69"
          kalicluster.vm.network "private_network", ip: "192.168.50.7"
          # kalicluster.vm.network "forwarded_port", guest: 80, host: 81
          #Disabling the default /vagrant share can be done as follows:
          # kalicluster.vm.synced_folder ".", "/vagrant", disabled: true
          kalicluster.vm.provider "virtualbox" do |vb|
              vb.name = "vbox-rsyslog-02"
              vb.memory = "768"
              vb.gui = false
          end
          # kalicluster.vm.provision "shell",    inline: "hostnamectl set-hostname vg-kali-05"
          # kalicluster.vm.provision "shell", inline: $centos_stream_docker_script
          kalicluster.vm.provision "shell", inline: $rsyslog_centos_stream8_script         
           
        end



end
