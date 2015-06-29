# vagrant Ubuntu 14.04 server, provision with puppet. 
Set up vagrant, run Ubuntu 14.04 server and provision with puppet to install apache, php, mysql and create virtual hosts.

## Install Vagrant.

[Download Vagrant](https://www.vagrantup.com/downloads.html)

## Install puppet open source.

http://docs.puppetlabs.com/guides/install_puppet/pre_install.html

## Install from [puppet forge](https://forge.puppetlabs.com/) apache and mysql.
```bash
$	puppet module install puppetlabs-apache
$	puppet module install puppetlabs-mysql
```

## Puppet [cheat sheet](https://docs.puppetlabs.com/puppet_core_types_cheatsheet.pdf).

## Usage.

1.	Replace "pathtofolder" with the path of your development directory in the vagranfile line: 
```ruby
config.vm.synced_folder "~/pathtofolder/", "/var/vagrant_hosts" 
```

2.	replace your username on the line below: (if modules directory doesn't exist you have to create it<sup>1</sup>).
```ruby
puppet.module_path = "/Users/yourusername/.puppet/modules"
```

<sup>1</sup>you can find the module_path running the following command:
```bash
$ puppet apply --configprint modulepath
```
If you want to create another vhost, in the puppet manifest, copy and paste the vhost resource description and modify it to your needs.

