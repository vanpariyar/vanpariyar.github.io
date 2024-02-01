---
title: "How to setup Linode VPS server"
slug: "how-to-setup-linode-vps-server"
date: 2023-11-09T10:14:11+05:30
image : "https://ia600508.us.archive.org/25/items/blog-images_202309/how-to-setup-linode-vps.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["VPS Server", "Shell Script"]
# meta description
description: "This is the commands that i use to setup Linode, Digital Ocean server, AWS VPS server"
keywords: ["Linode Server Setup", "Setup VPS easily"]
# save as draft
draft: false  
---

Hello everyone, :wave:
# Linode Server Setup Commands
> This blog post will cover the basic steps involved in setting up a Linode server using the following shell script:

If you want to use the Linode server [here is a link](https://www.linode.com/lp/refer/?r=002e869d999313a764652d3f6a833ea7b1cdbb09), You will receive some credits in your account

```shell
linode-server-setup-commands.sh

adduser hari
usermod -aG sudo hari
ufw app list
ufw allow OpenSSH
ufw enable
rsync --archive --chown=hari:hari ~/.ssh /home/hari
## install apache2
sudo apt update
sudo apt install apache2
sudo ufw app list
sudo ufw allow in "Apache"
sudo ufw status
#Mysql
sudo apt install mysql-server
sudo apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip
sudo systemctl restart apache2
```

## Step 1: Create a user and add them to the sudo group

The first step is to create a user account for yourself and add them to the sudo group. This will give you the ability to run commands with administrative privileges.

```shell
adduser hari
usermod -aG sudo hari
```

## Step 2: Enable the firewall

Next, we need to enable the firewall to protect our server from unauthorized access. We will also need to open a few ports to allow SSH traffic and Apache traffic.

```
ufw app list
ufw allow OpenSSH
ufw enable
```

## Step 3: Copy your SSH keys to the new user account

Now that we have created a new user account, we need to copy our SSH keys to that account so that we can log in using SSH.

```
rsync --archive --chown=hari:hari ~/.ssh /home/hari
```

## Step 4: Install Apache2

Next, we need to install the Apache2 web server.

```
sudo apt update
sudo apt install apache2
```

## Step 5: Enable Apache2 in the firewall

Now that Apache2 is installed, we need to enable it in the firewall so that it can receive traffic.

```
sudo ufw app list
sudo ufw allow in "Apache"
```

## Step 6: Install MySQL

MySQL is a popular database management system that is often used with Apache2.

```
sudo apt install mysql-server
```

## Step 7: Install PHP modules

PHP is a popular programming language that is often used to develop web applications. We need to install a few PHP modules so that our web applications can function properly.

```
sudo apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip
```

## Step 8: Restart Apache2

Finally, we need to restart Apache2 so that the changes we made take effect.

```
sudo systemctl restart apache2
```

## Conclusion

Once you have followed these steps, your Linode server will be ready to use. You can now start developing and deploying web applications.

Thanks For Reading 🙏

> This articles is generated Manually from generative AI, But carefully reviewed by Me personally. Please let me know if you found any issues, in comment section below.

{{< footer-donation >}}