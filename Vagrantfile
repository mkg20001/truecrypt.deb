$root_provision = <<SCRIPT
export DEBIAN_FRONTEND=noninteractive
apt-get update
apt-get install -y git gnupg2 vim
apt-get install -y devscripts debhelper pkg-config libgtk2.0-dev libfuse-dev nasm libappindicator-dev bash-completion
SCRIPT

$user_provision = <<SCRIPT
echo "Downloading truecrypt_7.1a.orig.tar.gz"
wget -q https://launchpad.net/~stefansundin/+archive/ubuntu/truecrypt/+files/truecrypt_7.1a.orig.tar.gz
tar xzf truecrypt_7.1a.orig.tar.gz
cd truecrypt-7.1a-source
ln -s /vagrant debian
wget -O debian/wxWidgets-2.8.12.tar.gz https://github.com/wxWidgets/wxWidgets/releases/download/v2.8.12/wxWidgets-2.8.12.tar.gz
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.hostname = "truecrypt.deb"
  config.vm.provision "shell", inline: $root_provision
  config.vm.provision "shell", inline: $user_provision, privileged: false
  config.vm.post_up_message = <<EOF
Run `vagrant ssh`, then run:
cd truecrypt-7.1a-source
debuild -i -us -uc -b

To copy the finished deb file out of the VM, run:
cp ../truecrypt_7.1a-8_amd64.deb /vagrant/
EOF
end
