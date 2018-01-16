# WordPress One-Click Install on DigitalOcean

## If you don't have one SSH key already set

[Generating a new ssh key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key)

## Digital Ocean Networking settings 

- Add new domain e.g: example.com **without the www**
- Set **A** records for example.com

```
HOSTNAME		WILL DIRECT TO
@			droplet-ip
*			droplet-ip
www			droplet-ip
test			droplet-ip
```

More at  [How to set up a host name with digitalocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-host-name-with-digitalocean)

## Set new Digital Ocean WordPress droplet WITH ssh login

[How to use the wordpress one click install on digitalocean](https://www.digitalocean.com/community/tutorials/how-to-use-the-wordpress-one-click-install-on-digitalocean)

## Set root UNIX password

`$ passwd`

## Configured with SSL using Let's Encrypt certificates and Certbot

### Install
On Ubuntu systems, the Certbot team maintains a PPA. Once you add it to your list of repositories all you'll need to do is apt-get the following packages.

```
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apt-get install python-certbot-apache
```

**You can save and close the file by hitting Ctrl-X, followed by Y, and then Enter to confirm.**

### Obtaining an SSL Certificate

**Hot issue:** https://github.com/certbot/certbot/issues/5405#issuecomment-356498627

> Unfortunately, Let's Encrypt has stopped offering the mechanism that Certbot's Apache and Nginx plugins use to prove you control a domain due to a security issue. See https://community.letsencrypt.org/t/2018-01-11-update-regarding-acme-tls-sni-and-shared-hosting-infrastructure/50188 for more info.

So to get SSL Certificate run this: 

```
$ sudo certbot --authenticator webroot --installer apache -w /var/www/html -d example.com -w /var/www/html -d www.example.com
```


More at [Certonly enter a webroot](https://community.letsencrypt.org/t/certonly-enter-a-webroot/27442/2)


- Next it will ask for your email, "Enter email address (used for urgent renewal and security notices)"
- Then ask to agree to Terms of Service. **R: A**  
- Then ask to share your email with the Electronic Frontier
Foundation.  **R: Y**
- Then it will ask for Which virtual host would you like to choose? **R: 2**  
- Then it will ask for whether or not to redirect HTTP traffic to HTTPS, removing HTTP access. **R: 2**

Then you will see 
```
Congratulations! You have successfully enabled https://example.com, https://test.example.com, and https://www.example.com
```

At this point, you can see your site browser bar `https://www.example.com`, with **https** SSL.


# Appendix

## Add a new user, and add to the sudo group:

```
$ adduser newuser
$ usermod -a -G sudo newuser
```
**(optional) Specifying Explicit User Privileges**

`$ visudo`

add this new line `newuser ALL=(ALL:ALL) ALL`, and save. 

```
root    ALL=(ALL:ALL) ALL
newuser ALL=(ALL:ALL) ALL
```
**You can save and close the file by hitting Ctrl-X, followed by Y, and then Enter to confirm.**

More at: 
[How to add and delete users on ubuntu 16 04](https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-ubuntu-16-04)
[Initial server setup with ubuntu 16-04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04)


## Workflow with git

Generate ssh key in the server

[Generating a new ssh key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key)

Copy `cat ~/.ssh/id_rsa.pub`

Add to github ssh keys. https://github.com/settings/keys

`git clone git@github.com:repository-name.git .` 

The folder must be empty.

Take into account the dot at the end of the line, `git clone git@github.com:repository-name.git .`, That is for clone in the same folder, e.g you are in /www/html, then clone the repository as I say previously, and all the files will be there without repository folder name.    


**When you update the repository in github, to update the server files, only do `git pull`, you will see the last changes.**    


## PhpMyAdmin

[How to install and secure phpmyadmin on ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-16-04)


## Redis

https://askubuntu.com/questions/868848/how-to-install-redis-on-ubuntu-16-04
