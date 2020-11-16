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
  config.vm.box = "bento/ubuntu-16.04"

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

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true

    # Customize the amount of memory on the VM:
    vb.memory = "8192"

    # Customize the number of cpus:
    vb.cpus = 6
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get upgrade -y
    apt-get autoremove -y

    # Editor
    apt-get install -y emacs dbus-x11

    # Build tools
    apt-get install -y build-essential cmake

    # Cliver-related packages
    apt-get install -y g++ curl python-minimal git bison flex bc libcap-dev
    apt-get install -y python-scapy python-libpcap expect

    # Boost needs the following:
    apt-get install -y libbz2-dev python-dev

    # LLVM needs the following:
    apt-get install -y libffi-dev

    # Klee-uclibc needs the following:
    apt-get install -y libncurses5-dev libncurses5

    # CryptoMiniSat4 needs:
    apt-get install -y valgrind libm4ri-dev libmysqlclient-dev libsqlite3-dev

    # Facebook Folly needs:
    apt-get install -y g++ automake autoconf autoconf-archive
    apt-get install -y libtool libboost-all-dev libevent-dev
    apt-get install -y libdouble-conversion-dev libgoogle-glog-dev libgflags-dev
    apt-get install -y liblz4-dev liblzma-dev libsnappy-dev make zlib1g-dev
    apt-get install -y binutils-dev libjemalloc-dev libssl-dev libiberty-dev

    # X11 for Xpilot
    apt-get install -y libx11-dev libxt-dev xorg-dev

    # BoringSSL needs:
    apt-get install -y ninja-build golang

    # update.sh build script needs:
    apt-get install -y lockfile-progs

    # R needs:
    # The version of R that comes with Ubuntu 16.04 can no longer pull all the
    # required packages. We therefore use a more recent version of R.
    # References:
    # 1. https://www.digitalocean.com/community/tutorials/how-to-install-r-on-ubuntu-16-04-2
    # 2. https://cran.r-project.org/bin/linux/ubuntu/README.html
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
    add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu xenial-cran40/'
    apt-get update
    apt-get install -y r-base r-base-dev r-recommended
    R -e 'install.packages("ggplot2", repos = "http://cran.us.r-project.org")'
    R -e 'install.packages("plyr", repos = "http://cran.us.r-project.org")'
    R -e 'install.packages("reshape", repos = "http://cran.us.r-project.org")'
    R -e 'install.packages("scales", repos = "http://cran.us.r-project.org")'
    R -e 'install.packages("quantreg", repos = "http://cran.us.r-project.org")'
    R -e 'install.packages("pastecs", repos = "http://cran.us.r-project.org")'
    R -e 'install.packages("xtable", repos = "http://cran.us.r-project.org")'

    # If you want the experiments scripts to be able to generate pdf
    # output (as opposed to png output), you need pdflatex.
    apt-get install -y texlive-base

    # Set umask globally
    echo umask 022 > /etc/profile.d/umask.sh
    chmod 644 /etc/profile.d/umask.sh
    umask 022

    # Add ssh host keys to known_hosts (MITM risk on first use here)
    # ssh-keyscan -H github.com >> /home/vagrant/.ssh/known_hosts
    # chown vagrant:vagrant /home/vagrant/.ssh/known_hosts

    # Playpen directory
    # ln -sfn /vagrant/playpen /playpen

  SHELL
end
