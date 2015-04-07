# vagrant-puppet-demo
Basic set up with vagrant for virtual machines and puppet as server provisioning.

## Install Vagrant.

[Download Vagrant](https://www.vagrantup.com/downloads.html)

## Install puppet open source.

http://docs.puppetlabs.com/guides/install_puppet/pre_install.html

## Install from [puppet forge](https://forge.puppetlabs.com/) apache and mysql.

$	puppet module install puppetlabs-apache

$	puppet module install puppetlabs-mysql


## Puppet [cheat sheet](https://docs.puppetlabs.com/puppet_core_types_cheatsheet.pdf).

## Usage.

1.	Replace "pathtofolder" with the path of your development directory in the vagranfile line: config.vm.synced_folder "~/pathtofolder/", "/var/vagrant_hosts" 

2.	replace your username on the line: (if modules directory doesn't exist you have to create it).
puppet.module_path = "/Users/yourusername/.puppet/modules"

you can find the module_path running the following command:
$ puppet apply --configprint modulepath

If you want to create another vhost, in the puppet manifest, copy and paste the vhost resource description, modify it to your needs and remove the require attribute.

