Vagrant Config for Apache, Mysql, PHP, phpMyadmin on Centos 6.4
Mysql datadir changed to a shared folder.

Installation:
==============
- install VirtualBox: https://www.virtualbox.org/wiki/Downloads
- install Vagrant: http://downloads.vagrantup.com/
- Download the Config.
    - change the shared folder settings in : *Vagrantfile* and *puppets/hierdata/common.yaml*
- run **vagrant plugin install vagrant-vbguest --plugin-source http://rubygems.org/ --plugin-version 0.10.0.pre1**
- run **vagrant up**
if provisioners not running run **vagrant provision**

if all is done, connect to the virtual host.
**vagrant ssh**

Because we changed the mysql datadir to a shared folder, mysql password is set in configs but not set on installation.
if you need, set a new root password for mysql:

- **mysqladmin -u root password 'newpassword'**


if you need phpmyadmin copy all from extras/phpmyadmin.php to  */etc/phpMyAdmin/config.inc.php*


thanks to:
=======

- http://www.puphpet.com because config is created with puphpet
- tayworm from the vagrant irc channel
- and google :)


known Issues:
=============
    vhost configs are removed after vagrant provision



