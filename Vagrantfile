# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "ci_cd_centos" do |config|
    config.vm.box = "centos/7"

    config.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)", auto_config: false

    config.vm.network "private_network", ip: "192.168.15.200"
    config.vm.provision "shell", run: "always", inline: "ip addr add 192.168.15.200 dev eth1"

    config.ssh.insert_key = false
    config.ssh.forward_agent = true
    config.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa']
    config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
    config.vm.provision "shell", inline: <<-EOC
      sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
      sudo systemctl restart sshd.service
      echo "finished"
    EOC
  end

  config.vm.define "ci_cd_ubuntu" do |config|
    config.vm.box = "ubuntu/bionic64"

    config.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)", auto_config: false

    config.vm.network "private_network", ip: "192.168.15.201"
    config.vm.provision "shell", run: "always", inline: "ip addr add 192.168.15.201 dev enp0s3"

    config.ssh.insert_key = false
    config.ssh.forward_agent = true
    config.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa']
    config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
    config.vm.provision "shell", inline: <<-EOC
      sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
      sudo systemctl restart ssh
      echo "finished"
    EOC
  end

end
  