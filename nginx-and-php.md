# Centos 7, Nginx and PHP configurations:

How to install multiples PHP versions for CentOS. For example the common is to __have 5.6 & 7.2 PHP versions__

Usefull commands, check for the PHP FPM Process

```
# Num of proceses
pgrep -fa php-fpm

# Check the location of socket
grep php /proc/net/unix

# Check Status
service php-fpm status

# Search for config
find / -type f -name "www.conf"
```

Install PHP 72 on CentOS

```

# Enable the repo
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
yum install yum-utils
yum-config-manager --enable remi-php72
yum update

# Install the PHP 7.2
yum install php72

# Install Dependencies
yum install php72-php-fpm php72-php-gd php72-php-json php72-php-mbstring php72-php-mysqlnd php72-php-xml php72-php-xmlrpc php72-php-opcache

# Check installed version and available extensions
php72 --modules
php72 --version

# Search for more modules and shit...
yum search php72 | more
yum search php72 | egrep 'fpm|gd|mysql|memcache'

```

## What if php -v show other version, how to enable the 7.2:

Then you use multiple PHP versions

```
yum install php72-php-cli
php72 -v
scl enable php72 bash
php -v
```

If you are using only one PHP version:

```
yum-config-manager --enable remi-php72
yum update
yum install php-cli
php -v
```

# Install the PHP 5.6 Version:

```
yum install php56 php56-php-common php56-php-fpm
yum-config-manager --enable remi-php56

# Install some extensions
yum install php56-php-mysql php56-php-pecl-memcache php56-php-pecl-memcached php56-php-gd php56-php-mbstring php56-php-mcrypt php56-php-xml php56-php-pecl-apc php56-php-cli php56-php-pear php56-php-pdo
```

# Check the config and update this values:

```
# Find files
find / -type f -name "www.conf"

# PHP 5.6
listen = 127.0.0.1:9001

# PHP 7.2
listen = 127.0.0.1:9000

# Also dont forget:
user = nginx
group = nginx
```

# Enable and restart services

```
systemctl enable php56-php-fpm 
systemctl enable php72-php-fpm 


systemctl start php56-php-fpm
systemctl start php72-php-fpm 

systemctl status php56-php-fpm
systemctl status php72-php-fpm 

```

# The NGINX config should be:

```
fastcgi_pass   127.0.0.1:9000; PHP72
fastcgi_pass   127.0.0.1:9001; PHP56
```