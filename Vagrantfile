Vagrant.configure(2) do |config|
  config.vm.provider "virtualbox" do |v|
    v.name = "opentripplanner"
    v.memory = 5120
    v.cpus = 2
  end

  config.vm.box = "envimation/ubuntu-xenial-docker"
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    ln -s /vagrant/data /home/vagrant/data
    docker pull urbica/otp
    echo "docker run --rm -e JAVA_MX=4G -v /home/vagrant/data:/data:ro -p 8080:8080 urbica/otp --build /data --pointSets /data --inMemory --server --analyst" > /home/vagrant/start
    # docker pull goabout/opentripplanner
    # echo "docker run --rm -e JAVA_MX=4G -v /home/vagrant/data:/data:ro -p 8080:8080 goabout/opentripplanner otp --build /data --pointSets /data --inMemory --server --analyst" > /home/vagrant/start
    chmod 755 /home/vagrant/start
    chown vagrant:vagrant /home/vagrant/start
  SHELL
end
