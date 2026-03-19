# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "debian" do |demo|
    demo.vm.box = "debian"
    demo.vm.hostname = "slave"
    demo.vm.network "private_network", ip: "192.168.100.4", netmask: "255.255.255.240", virtualbox__intnet: "reto3"
    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "512"
    end
  end
end


Vagrant.configure("2") do |config|

  config.vm.define "debian2" do |demo|
    demo.vm.box = "debian2"
    demo.vm.hostname = "GitHub"
    demo.vm.network "private_network", ip: "192.168.100.4", netmask: "255.255.255.240", virtualbox__intnet: "reto3"
    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "512"
      demo.vm.provision "shell", inline: <<-SHELL
      sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
      SHELL
    end
  end
end


Vagrant.configure("2") do |config|

  config.vm.define "ubuntu" do |demo|
    demo.vm.box = "ubuntu"
    demo.vm.hostname = "ubuntu"
    demo.vm.network "private_network", type: "dhcp", virtualbox__intnet: "reto3"
    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "2048"
    end
    demo.vm.provision "shell", inline: <<-SHELL
      sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
      sudo apt-get update
      sudo apt-get install -y ldap-utils
      sudo apt-get install -y libpam-ldap
      sudo apt-get install -y libnss-ldap
      sudo ip route add default via 192.168.100.1

    SHELL
  end
end

Vagrant.configure("2") do |config|

  config.vm.define "rocky" do |demo|
    demo.vm.box = "rocky"
    demo.vm.network "public_network", :bridge => "eth0", :adapter => 2
    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "512"
    end
  end
end

Vagrant.configure("2") do |config|

  config.vm.define "w10" do |demo|
    demo.vm.box = "w10"
    demo.vm.communicator = "winrm"
    demo.winrm.username = "vagrant"
    demo.winrm.password = "vagrant"
    demo.vm.network "private_network", type: "dhcp", virtualbox__intnet: "reto3"

    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "5120" 
    demo.vm.provision "shell", inline: <<-SHELL
      route /p add 192.168.100.32 mask 255.255.255.0 192.168.100.33
    SHELL
    end
  end
end

Vagrant.configure("2") do |config|

  config.vm.define "w2k19" do |demo|
    demo.vm.box = "w2k19"
    demo.vm.communicator = "winrm"
    demo.winrm.username = "vagrant"
    demo.winrm.password = "vagrant"
    demo.vm.provider "virtualbox" do |vb|
    demo.vm.network "public_network", :bridge => "eth0", :adapter => 2
      vb.gui = false
      vb.memory = "2042"
    end
  end
end


Vagrant.configure("2") do |config|

  config.vm.define "router1" do |demo|
    demo.vm.box = "debian"
    demo.vm.hostname = "router"
    demo.vm.network "private_network", ip: "192.168.100.1", netmask: "255.255.255.240", virtualbox__intnet: "reto3"
    demo.vm.network "public_network", ip: "172.25.208.12", netmask: "255.255.0.0"
    demo.vm.network "private_network", ip: "192.168.100.129", netmask: "255.255.255.248", virtualbox__intnet: "admin3"
    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "511"
    end
    demo.vm.provision "shell", inline: <<-SHELL
      sudo ip route del default
      sudo ip route add default via 172.25.130.254
      sudo ip route flush 192.168.100.0/24
      sudo ip route add 192.168.100.0/28 via 172.25.208.12 dev enp0s9
      sudo ip route add 192.168.100.16/28 via 172.25.215.12 dev enp0s9
      sudo ip route add 192.168.100.32/27 via 172.25.212.12 dev enp0s9
      sudo ip route add 192.168.100.64/26 via 172.25.205.12 dev enp0s9
      sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
    # sudo apt-get update
    # sudo apt-get install vim -y
    # sudo apt-get install isc-dhcp-server -y
    # sudo apt-get install iptables -y
    # sudo cp /vagrant/dhcpd.conf /etc/dhcp/dhcpd.conf
    # sudo echo 'INTERFACESv4="enp0s8"' | sudo tee /etc/default/isc-dhcp-server
    # sudo systemctl restart isc-dhcp-server
    SHELL
  end
end

Vagrant.configure("2") do |config|

  config.vm.define "router2" do |demo|
    demo.vm.box = "debian"
    demo.vm.network "private_network", ip: "192.168.100.17", netmask: "255.255.255.240", virtualbox__intnet: "reto3"
    demo.vm.network "public_network", ip: "172.25.215.12", netmask: "255.255.0.0"
    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "511"
    end
    demo.vm.provision "shell", inline: <<-SHELL
      sudo ip route del default
      sudo ip route add default via 172.25.130.254
      sudo ip route flush 192.168.100.0/24
      sudo ip route add 192.168.100.0/28 via 172.25.208.12 dev enp0s9
      sudo ip route add 192.168.100.16/28 via 172.25.215.12 dev enp0s9
      sudo ip route add 192.168.100.32/27 via 172.25.212.12 dev enp0s9
      sudo ip route add 192.168.100.64/26 via 172.25.205.12 dev enp0s9
      sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
      sudo apt-get update
      sudo apt-get install vim -y
      sudo apt-get install isc-dhcp-server -y
      sudo apt-get install iptables -y
      sudo cp /vagrant/dhcpd.conf /etc/dhcp/dhcpd.conf
      sudo echo 'INTERFACESv4="enp0s8"' | sudo tee /etc/default/isc-dhcp-server
      sudo systemctl restart isc-dhcp-server
      sudo apt-get install vim -y
    SHELL
  end
end


Vagrant.configure("2") do |config|

  config.vm.define "router3" do |demo|
    demo.vm.box = "debian"
    demo.vm.network "private_network", ip: "192.168.100.33", netmask: "255.255.255.224", virtualbox__intnet: "reto3"
    demo.vm.network "public_network", ip: "172.25.212.12", netmask: "255.255.0.0"
    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "511"
    end
    demo.vm.provision "shell", inline: <<-SHELL
      sudo ip route del default
      sudo ip route add default via 172.25.130.254
      sudo ip route flush 192.168.100.0/24
      sudo ip route add 192.168.100.0/28 via 172.25.208.12 dev enp0s9
      sudo ip route add 192.168.100.16/28 via 172.25.215.12 dev enp0s9
      sudo ip route add 192.168.100.32/27 via 172.25.212.12 dev enp0s9
      sudo ip route add 192.168.100.64/26 via 172.25.205.12 dev enp0s9
      sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
      sudo apt-get update
      sudo apt-get install vim -y
      /home/ilecina/vagrant/dhcpd.conf
      sudo apt-get install vim -ysudo apt-get install isc-dhcp-server -y
      sudo apt-get install iptables -y
      sudo cp /vagrant/dhcpd.conf /etc/dhcp/dhcpd.conf
      sudo echo 'INTERFACESv4="enp0s8"' | sudo tee /etc/default/isc-dhcp-server
      sudo systemctl restart isc-dhcp-server
    SHELL
  end
end

Vagrant.configure("2") do |config|

  config.vm.define "router4" do |demo|
    demo.vm.box = "debian"
    demo.vm.network "private_network", ip: "192.168.100.65", netmask: "255.255.255.192", virtualbox__intnet: "reto3"
    demo.vm.network "public_network", ip: "172.25.205.12", netmask: "255.255.0.0"
    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "511"
    end
    demo.vm.provision "shell", inline: <<-SHELL
      sudo ip route del default
      sudo ip route add default via 172.25.130.254
      sudo ip route flush 192.168.100.0/24
      sudo ip route add 192.168.100.0/28 via 172.25.208.12 dev enp0s9
      sudo ip route add 192.168.100.16/28 via 172.25.215.12 dev enp0s9
      sudo ip route add 192.168.100.32/27 via 172.25.212.12 dev enp0s9
      sudo ip route add 192.168.100.64/26 via 172.25.205.12 dev enp0s9
      sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
      sudo apt-get update
      sudo apt-get install vim -y
      sudo apt-get install isc-dhcp-server -y
      sudo apt-get install iptables -y
      sudo cp /vagrant/dhcpd.conf /etc/dhcp/dhcpd.conf
      sudo echo 'INTERFACESv4="enp0s8"' | sudo tee /etc/default/isc-dhcp-server
      sudo systemctl restart isc-dhcp-server
    SHELL
  end
end

Vagrant.configure("2") do |config|

  config.vm.define "dnsftp" do |demo|
    demo.vm.box = "debian"
    demo.vm.hostname = "dnsftp"
    demo.vm.network "private_network", type: "dhcp", virtualbox__intnet: "reto3"
    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "511"
    end
    demo.vm.provision "shell", inline: <<-SHELL
      sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
      sudo apt-get update
      sudo apt-get install bind9 -y
      sudo apt-get install vsftpd -y
      sudo apt-get install -y vim
      sudo ip route del default
      sudo ip route add default via 192.168.100.1
      SHELL
  end
end

Vagrant.configure("2") do |config|

  config.vm.define "nfs" do |demo|
    demo.vm.box = "debian"
    demo.vm.hostname = "nfs"
    demo.vm.network "private_network", type: "dhcp", virtualbox__intnet: "reto3"
    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "511"
    end
    demo.vm.provision "shell", inline: <<-SHELL
      sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
      sudo apt-get update && sudo apt-get install nfs-kernel-server nfs-common -y
      sudo apt-get install -y vim
      sudo ip route del default
      sudo ip route add default via 192.168.100.1

      SHELL
  end

end

Vagrant.configure("2") do |config|

  config.vm.define "ldap" do |demo|
    demo.vm.box = "debian"
    demo.vm.hostname = "ldap"
    demo.vm.network "private_network", type: "dhcp", virtualbox__intnet: "reto3"
    demo.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "512"
    end
    demo.vm.provision "shell", inline: <<-SHELL
      sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
    # sudo apt-get update && sudo apt-get install slapd ldap-utils db4.8-util -y
    # sudo apt-get install -y vim
      sudo ip route del default
      sudo ip route add default via 192.168.100.1

    SHELL
  end
end
