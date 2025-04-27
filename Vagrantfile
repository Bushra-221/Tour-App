Vagrant.configure("2") do |config|

    #base box
    config.vm.box = "ubuntu/jammy64"
  
    #ssh access
    config.ssh.insert_key = false


    # Load Balancer
    config.vm.define "lb" do |lb|
      lb.vm.hostname = "load-balancer"
      lb.vm.network "private_network", ip: "192.168.70.100"
      lb.vm.provision "shell", path: "lb-setup.sh"
        vb.memory = 2048  # 2GB RAM
      end
  
    # Web Servers 
    (1..3).each do |i|
      config.vm.define "web#{i}" do |web|
        web.vm.hostname = "web#{i}"
        web.vm.network "private_network", ip: "192.168.70.10#{i}"
        config.vm.synced_folder "./frontend/build", "/var/www/tour-app"
        web.vm.provision "shell", inline: <<-SHELL
          vb.memory = 1024  # 1GB RAM

          at update 
          apt install -y nginx
          rm -rf /var/www/html
          ln -s /var/www/react-app /var/www/html
          systemctl restart nginx
          SHELL


        end
     # Provisioning to install dependencies and build the app
      web.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y nginx nodejs npm
      # Only build once (on first server)
      if [ ! -d "/vagrant/frontend/build" ]; then
        cd /vagrant/frontend
        npm install
        npm run build
      fi

      sudo rm -rf /var/www/html
      sudo ln -s /var/www/tour-app /var/www/html
    SHELL
      end
    end
  end
