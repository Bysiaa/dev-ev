# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_version = "20191107.0.0"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessible to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  # config.vm.synced_folder ".", "/vagrant", disabled: true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2

  # Pierwsza maszyna - Python Development
  config.vm.define "python-dev" do |python|
    python.vm.box = "ubuntu/trusty64"
    python.vm.box_version = "20191107.0.0"
    python.vm.hostname = "python-dev.local"

    python.vm.provider "virtualbox" do |vb|
      vb.memory = "8000"
      vb.cpus = 4
    end

    python.vm.provision "shell", inline: <<-SHELL
      echo "AKTUALIZUJE SYSTEM..."
      apt-get update -y
      apt-get upgrade -y

      echo "INSTALUJE PYTHONA3 I NARZĘDZIA DEVELOPERSKIE..."
      apt-get install -y python3 python3-pip python3-venv build-essential libssl-dev libffi-dev git
      pip3 install --upgrade pip
      pip3 install numpy pandas matplotlib jupyterlab black flake8 pytest

      echo "INSTALACJA POSTGRESQL..."
      apt-get install -y postgresql postgresql-contrib
      sudo -u postgres psql -c "CREATE USER vagrant WITH PASSWORD 'vagrant';"
      sudo -u postgres psql -c "ALTER USER vagrant CREATEDB;"

      echo "KONFIGURACJA JUPYTERLAB..."
      mkdir -p /home/vagrant/notebooks
      chown -R vagrant:vagrant /home/vagrant/notebooks
      echo 'alias jupyter="jupyter-lab --notebook-dir=/home/vagrant/notebooks --ip=0.0.0.0 --no-browser --allow-root"' >> /home/vagrant/.bashrc

      echo "TWORZENIE WIRTUALNEGO ŚRODOWISKA..."
      python3 -m venv /home/vagrant/python-env
      chown -R vagrant:vagrant /home/vagrant/python-env
      git clone https://github.com/waskagaska/us_cw/

      echo ">>> GOTOWE! Twój Python Development Environment jest przygotowany!" > /etc/motd
    SHELL

    python.vm.synced_folder "./python_projects", "/home/vagrant/python_projects"
  end

  # Druga maszyna - C++ Development
  config.vm.define "cpp-dev" do |cpp|
    cpp.vm.box = "ubuntu/trusty64"
    cpp.vm.box_version = "20191107.0.0"
    cpp.vm.hostname = "cpp-dev.local"

    cpp.vm.provider "virtualbox" do |vb|
      vb.memory = "6000"
      vb.cpus = 4
    end

    cpp.vm.provision "shell", inline: <<-SHELL
      echo "AKTUALIZUJE SYSTEM..."
      apt-get update -y
      apt-get upgrade -y

      echo "INSTALACJA NARZĘDZI DO C++..."
      apt-get install -y build-essential cmake gdb clang valgrind

      echo "INSTALACJA VS CODE..."
      snap install --classic code

      echo "INSTALACJA NARZĘDZI TERMINALOWYCH..."
      apt-get install -y tmux htop tree curl wget

      echo "TWORZENIE FOLDERU NA PROJEKTY..."
      mkdir -p /home/vagrant/cpp-projects
      chown -R vagrant:vagrant /home/vagrant/cpp-projects

      echo ">>> GOTOWE! Twoje środowisko C++ jest przygotowane!" > /etc/motd
    SHELL

    cpp.vm.synced_folder "./cpp_projects", "/home/vagrant/cpp_projects"
  end

end
