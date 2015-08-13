# -*- mode: ruby -*-
# vi: set ft=ruby :

# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty32"
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "private_network", ip: "10.10.10.10"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end
  config.vm.provision "file", source: "response.varfile", destination: "response.varfile"
  config.vm.provision "file", source: "supporting/mysql_connector.jar", destination: "mysql_connector.jar"
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
    sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
    sudo apt-get install -y vim curl python-software-properties
    sudo apt-get -y install mysql-server
    sudo sed -i "s/^bind-address/#bind-address/" /etc/mysql/my.cnf
    sudo mysql -u root -proot -e "CREATE DATABASE jira;"
    sudo mysql -u root -proot -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION; FLUSH PRIVILEGES;"
  sudo /etc/init.d/mysql restart
    wget -q https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-6.4.10-x32.bin
    chmod +x atlassian-jira-6.4.10-x32.bin
    sudo ./atlassian-jira-6.4.10-x32.bin -q -varfile response.varfile
    cp /home/vagrant/mysql_connector.jar /home/vagrant/atlassian/jira/lib/
    cd /home/vagrant/atlassian/jira/bin
    sudo ./stop-jira.sh
    sudo ./start-jira.sh
  SHELL
end
