# 安装
https://self-service-password.readthedocs.io/en/latest/installation.html


## From tarball
Prerequisites:

Apache or another web server

php (>=7.4)

php-curl (haveibeenpwned api)

php-filter

php-gd (captcha)

php-ldap

php-mbstring (reset mail)

php-openssl (token crypt, probably built-in)

Smarty (version >=3)

Tarball can be downloaded from LTB project website.

Uncompress and unarchive the tarball:

tar -zxvf ltb-project-self-service-password-*.tar.gz
Install files in /usr/share/:

mv ltb-project-self-service-password-* /usr/share/self-service-password
Adapt ownership of Smarty cache repositories so Apache user can write into them. For example:

chown apache:apache /usr/share/self-service-password/cache
chown apache:apache /usr/share/self-service-password/templates_c



## Debian / Ubuntu
Warning

You need to install first the package smarty3. If you face the error syntax error, unexpected token "class", try to install a newer version of the package:

# wget http://ftp.us.debian.org/debian/pool/main/s/smarty3/smarty3_3.1.47-2_all.deb

# dpkg -i smarty3_3.1.47-2_all.deb

Configure the repository:

vi /etc/apt/sources.list.d/ltb-project.list
deb [arch=amd64 signed-by=/usr/share/keyrings/ltb-project.gpg] https://ltb-project.org/debian/stable stable main
Import repository key:

wget -O - https://ltb-project.org/documentation/_static/RPM-GPG-KEY-LTB-project | gpg --dearmor | sudo tee /usr/share/keyrings/ltb-project.gpg >/dev/null
Then update:

apt update
You are now ready to install:

apt install self-service-password



# LDAP Tool Box Self Service Password

[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/372/badge)](https://bestpractices.coreinfrastructure.org/projects/372)
[![Build Status](https://travis-ci.org/ltb-project/self-service-password.svg?branch=master)](https://travis-ci.org/ltb-project/self-service-password)
[![Documentation Status](https://readthedocs.org/projects/self-service-password/badge/?version=latest)](https://self-service-password.readthedocs.io/en/latest/?badge=latest)

## Presentation

Self Service Password is a PHP application that allows users to change their password in an LDAP directory.

The application can be used on standard LDAPv3 directories (OpenLDAP, OpenDS, ApacheDS, Sun Oracle DSEE, Novell, etc.) and also on Active Directory.

![Screenshot](https://ltb-project.org/documentation/_images/ssp_1_0_change_password.png)

It has the following features:
* Samba mode to change Samba passwords
* Active directory mode
* Local password policy:
  * Minimum/maximum length
  * Forbidden characters
  * Upper, Lower, Digit or Special characters counters
  * Reuse old password check
  * Password same as login
  * Complexity (different class of characters)
* Help messages
* Reset by questions
* Reset by mail challenge (token sent by mail)
* Reset by SMS (trough external Email 2 SMS service or SMS API)
* Change SSH Key in LDAP directory
* Captcha (built-in)
* Mail notification after password change
* Hook script before and after password change

## Prerequisite

* PHP (>=7)
* PHP extensions required:
  * php-curl (haveibeenpwned api)
  * php-gd (captcha)
  * php-filter
  * php-ldap
  * php-mbstring (reset mail)
  * php-openssl (token crypt, probably built-in)
* Smarty 3
* strong cryptography functions available (for random_compat, PHP 7 or libsodium or /dev/urandom readable or php-mcrypt extension installed)
* valid PHP mail server configuration (reset mail)
* valid PHP session configuration (reset mail)

## Documentation

Documentation is available on https://self-service-password.readthedocs.io/en/latest/

## Docker

We provide an [official Docker image](https://hub.docker.com/r/ltbproject/self-service-password).

Create a minimal configuration file:
```
vi ssp.conf.php
```
```php
<?php // My SSP configuration
$keyphrase = "mysecret";
$debug = true;
?>
```

And run:
```
docker run -p 80:80 \
    -v $PWD/ssp.conf.php:/var/www/conf/config.inc.local.php \
    -it docker.io/ltbproject/self-service-password:latest
```

## Download

Tarballs and packages for Debian and Red Hat are available on https://ltb-project.org/download.html

Debian and Red Hat repositories are also available, see [installation instructions](https://self-service-password.readthedocs.io/en/latest/installation.html).

## Source code

Source codes are available on https://github.com/ltb-project/self-service-password
