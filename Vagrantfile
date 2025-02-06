Vagrant.configure("2") do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.box_check_update = false
  config.vm.box = "bento/ubuntu-22.04"
  config.vm.hostname = "coolify-vm"

  # Provision SSH key
  config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/EosLab/VirtualMachines/coolify-server/keys/coolify_key.pub").first.strip
    s.inline = <<-SHELL
    mkdir -p /home/vagrant/.ssh
    echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
    chmod 600 /home/vagrant/.ssh/authorized_keys
    SHELL
  end

  config.vm.define "vbox" do |vbox|
    vbox.vm.network "private_network", ip: "192.168.56.10"
    vbox.vm.provider "virtualbox" do |vb|
      vb.memory = "8192"
      vb.cpus = 4
      vb.name = "coolify-vm"
    end
  end

  # config.vm.provision "ansible" do |ansible|
  #   ansible.playbook = "ansible/install-coolify.yml"
  #   ansible.inventory_path = "ansible/inventory.ini"
  # end
end


# to access the Coolify dashboard http://192.168.56.20:8000 (admin-coolify / root....)
