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

## Set up Vagrantfile.
+   Open Vagrantfile.
+   Replace `pathtofolder` with the path of your development directory (usually `/var/www/vhosts/`) on the line:
```ruby
config.vm.synced_folder "~/pathtofolder/", "/var/www/vhosts" 
```
The result will be that your `vhost` folder or any other folder, where you host all your projects will be mapped to `/var/www/vhosts`, how to set up a virtual host for your directory or project is describe below ("Set up puppet manifest file").

+  replace your username on the line below: (if modules directory doesn't exist you have to create it<sup>1</sup> ).
```ruby
puppet.module_path = "/Users/yourusername/.puppet/modules"
```
<sup>1</sup>you can find the `module_path` running the following command on the terminal:
```bash
$ puppet apply --configprint modulepath
```

+   (Optional) On the line `config.vm.network "private_network", ip: "192.168.33.10"` change the ip address if you are gonna run a new instance with the same box and the same vagrantfile (or you can use only one environment for all your projects (adding virtual hosts for each one, but I don't recommend it).

## Set up Puppet manifest file.
+   go to the folder manifests and open default.pp
+   To create a virtual host, on the code below change `local.example.com` to your "local.domainname.com". Change `vgdemo` on `/var/www/vhosts/vgdemo`(remeber that vagrant syncs your dev path with /var/www/vhosts/) to your whatever name your project has. Copy the code below and repeat the above if you want to add another vhost.
```ruby
apache::vhost{"local.example.com":  
    port    => '80',
    docroot => '/var/www/vhosts/vgdemo',
    directories => [{
                    path => '/var/www/vhosts/vgdemo',
                    options => 'All',                                       
                    allow_override => ['All'],
                    custom_fragment => 'Order allow,deny
                    Allow from all',
                    },],    
}
```

+ change the following code for your own needs to create a database:
```ruby
mysql::db { 'mydb':
    user     => 'myuser',
    password => 'mypass',
    host     => 'localhost',
    grant    => ['ALL'],
}
```
## Run Vagrant
+   After you followed the above instructtions, open the terminal, go to the root of this repo, and run:
`$ vagrant up`

+   if you changed the default.pp file, to provision your enviroment run:
`$  vagrant provision`.

