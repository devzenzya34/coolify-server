Vagrant.configure("2") do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.box_check_update = false
  config.vm.box = "bento/ubuntu-24.04"

  # Provision SSH key
  config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
    mkdir -p /home/vagrant/.ssh
    echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
    chmod 600 /home/vagrant/.ssh/authorized_keys
    SHELL
  end

  config.vm.define "vbox" do |vbox|
    vbox.vm.hostname = "coolify-vm"
    vbox.vm.network "private_network", ip: "192.168.56.40"
    vbox.vm.network "public_network", ip: "192.168.1.40", bridge: "enp3s0" 
    vbox.vm.provider "virtualbox" do |vb|
      vb.memory = "8192"
      vb.cpus = 4
      vb.customize ["modifyvm", :id, "--uartmode1", "disconnected"]
    end
  end
end


# to access the Coolify dashboard http://192.168.56.20:8000 (admin-coolify / root....)
