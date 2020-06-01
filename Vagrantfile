Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--uart1", "0x3F8", "4"]
    vb.customize ["modifyvm", :id, "--uartmode1", "file", "./ttyS0.log"]
    vb.memory = "4096"
  end
  config.vm.network "forwarded_port", guest: 3002, host:3002
  config.vm.synced_folder "/Users/mani47/Projects", "/home/vagrant/Projects", type: "virtualbox"
  config.vm.synced_folder "/Users/mani47/.ssh", "/home/vagrant/.ssh", type: "virtualbox"
  config.vm.boot_timeout = 600
  config.vm.provision "shell", inline: <<-SHELL
  sudo apt-get update
  sudo apt-get install -y autoconf bison build-essential curl g++ gcc git libffi-dev libgconf-2-4 libgdbm-dev libncurses5-dev libreadline-dev libsqlite3-dev libssl-dev libxi6 libyaml-dev make sqlite3 xvfb zip zlib1g-dev postgresql-client libsasl2-dev libpq-dev zsh amazon-ecr-credential-helper
  sudo apt-get install -y \
      apt-transport-https \
      ca-certificates \
      curl \
      gnupg-agent \
      software-properties-common
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  sudo apt-key fingerprint 0EBFCD88
  sudo add-apt-repository \
     "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
     $(lsb_release -cs) \
     stable"
  sudo apt-get update
  sudo apt-get install -y docker-ce docker-ce-cli containerd.io
  sudo usermod -aG docker vagrant
  curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
  curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
  sudo apt-get install -y nodejs
  sudo apt-get update && sudo apt-get install yarn
  gpg --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
  \curl -sSL https://get.rvm.io | bash -s stable
  source /home/vagrant/.rvm/scripts/rvm
  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
  unzip awscliv2.zip
  sudo ./aws/install
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
  sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose
  echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
  SHELL
end
