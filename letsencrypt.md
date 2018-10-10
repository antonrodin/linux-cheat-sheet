LetsEncryps
===========

CheatSheet for LetsEncrypt Certificates for Nginx, Apache webservers on Ubuntu or Centos.

## CentOs && Nginx

```shell
sudo yum install epel-release
sudo yum install certbot-nginx
sudo certbot --nginx -d example.com -d www.example.com

# Test Nginx Config and Reload
sudo nginx -t
sudo systemctl reload nginx

# Set up automatic renew
sudo crontab -e

# Paste there and save file
15 3 * * * /usr/bin/certbot renew --quiet
```

## Ubuntu && Apache
https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-16-04

```shell
# Get repo update & Install
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python-certbot-apache

# Config LetsEncryps para tile.azr.es
sudo certbot --apache -d example.com -d www.example.com
```

### You can allways test the authomatic renew of the certificate

```shell
sudo certbot renew --dry-run
```

It add some modification into this file, you can 000-default.conf, depends if you check redirect or not...