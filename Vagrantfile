Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024 
    vb.cpus = 2
    vb.name = "dev_ubuntu_nodejs"
  end

  config.vm.define "ubuntuNodejs" do |ubuntuNodejs|
    ubuntuNodejs.vm.network "public_network", ip: "192.168.87.28", use_dhcp_assigned_default_route: true
    ubuntuNodejs.vm.network "forwarded_port", guest:3000, host:8089
    
    
    ubuntuNodejs.vm.synced_folder "./configs", "/configs"
    ubuntuNodejs.vm.synced_folder ".", "/vagrant", disabled: true

    
    ubuntuNodejs.vm.provision "shell",
      inline: "apt install curl && \
      curl -fsSL https://deb.nodesource.com/setup_14.x | bash - && \
      apt-get install -y nodejs"

    ubuntuNodejs.vm.provision "shell",
      inline: "cat /configs/auth/auth_teamdev_ubuntu_key.pub >> .ssh/authorized_keys"

    ubuntuNodejs.vm.provision "shell",
      inline: "npm install --global yarn"

    ubuntuNodejs.vm.provision "shell",
      inline: "apt-get install git"
    
    ubuntuNodejs.vm.provision "shell",
      inline: "mkdir projeto1 && \
      cd projeto1 && \
      git clone https://github.com/Orifiel/GitHub_Explorer.git && \
      cd GitHub_Explorer && \
      yarn && yarn start"

  

  end

end