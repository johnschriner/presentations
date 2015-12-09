#How To Set Up the Latest MediaWiki with Lighttpd on Ubuntu 14.04

##Introduction

MediaWiki is a popular open source wiki platform that can be used for public or internal collaborative content publishing. MediaWiki is used for many of the most popular wikis on the internet including Wikipedia, the site that the project was originally designed to serve.

In this guide, we will be setting up the latest version of MediaWiki on an Ubuntu 14.04 server. We will use the lighttpd web server to make the actual content available, php-fpm to handle dynamic processing, and mysql to store our wiki's data.
##Prerequisites


To complete this guide, you should have access to a clean Ubuntu 14.04 server instance. On this system, you should have a non-root user configured with sudo privileges for administrative tasks. You can learn how to set this up by following our Ubuntu 14.04 initial server setup guide.

When you are ready to continue, log into your server.  We will be connected through a terminal to our server via SSH.  More information on SSH can be found [here](https://www.digitalocean.com/community/tutorials/how-to-connect-to-your-droplet-with-ssh).  As we're going to be installing software, make sure you either enter the following and then your root password for administrator privileges or simply type sudo before each command in this tutorial:

        sudo su


It's good practice to make certain that your system is up to date with:

        sudo apt-get update
        sudo apt-get upgrade

##Install the Server Components
As we're not using Apache as part of the **L**inux, **A**pache, **M**ySQL, **P**HP (LAMP) package, we're going to install each component separately.

###Installing Lighttpd
Lighttpd (pronounced *Lighty*) webserver is highly efficient, quick, and easy to install.
Install Lighttpd using apt-get:

        sudo apt-get install lighttpd
After installation, the web server will automatically start.  Simply point your browser to your Droplet's public IP address and the placeholder page with show up at the default port 80.
This welcome page explains that configuration files can be found in the directory:

        /etc/lighttpd

The document root directory is by default:

        /var/www

Lighttpd can be admininistered from the command line by using the following:

        sudo service lighttpd start
        sudo service lighttpd stop
        sudo service lighttpd restart
        
###Installing MySQL Server
Next, we'll install and configure MySQL database to store the information for the wiki.
Install the newest MySQL using apt-get:

        sudo apt-get install mysql-server
You will be asked to create a root password.  Make sure to remember it or place it in a password manager; we'll need the root password to create an account for MediaWiki.

MySQL service will start automatically but to check that the service has opened a port you can try:

        nmap localhost

MySQL will have port 3306 opened.

![nmap shows us which ports are open](http://i.imgur.com/wIfVYNb.png)

 
As MySQL is a service like lighttpd, it can be administered from the command line:

        sudo service mysql start
        sudo service mysql stop                
        sudo service mysql restart
        
Install PHP and FPM (FastCGI Process Manager) with:

        apt-get install php5-cli php5-cgi php5-mysql php-fpm

PHP-FPM is an alternative to Lighttpd's spawn-fcgi PHP FastCGI implementation.  Essentially, with its adaptive process spawning it helps to handle traffic for busy sites.  We'll configure this further below.

After installation we can verify it was properly installed and get the version number:

        php -v
++++++++ADD other PHP check method+++++++
        
##Configure MySQL and Create Credentials for MediaWiki
Log into MySQL as root:

        mysql -u root -p
At the mysql prompt now, we can add do the following to create a user:

        CREATE DATABASE mediawikidb;
        CREATE USER mediawikiuser@localhost IDENTIFIED BY 'mediawikipassword';
        GRANT index, create, select, insert, update, delete, alter, lock tables on mediawikidb.* TO mediawikiuser@localhost;
        FLUSH PRIVILEGES;
        exit

##Configure Lighttpd and PHP-FPM
We now need to configure Lighttpd to use PHP-FPM instead of spawn-fcgi.
To do this, cd to Lighttpd's configuration file directory:

        cd /etc/lighttpd/conf-available/
Then make a backup copy of 15-fastcgi-php.conf

        cp 15-fastcgi-php.conf 15-fastcgi-php-spawnfcgi.conf
Now, we'll edit the old 15-fastcgi-php.conf:

        nano 15-fastcgi-php.conf

Edit this file to now read:

        # /usr/share/doc/lighttpd-doc/fastcgi.txt.gz
        # http://redmine.lighttpd.net/projects/lighttpd/wiki/Docs:ConfigurationOptions#mod_fastcgi-fastcgi
        
        ## Start an FastCGI server for php (needs the php5-cgi package)
        fastcgi.server += ( ".php" =>
                ((
                "socket" => "/var/run/php5-fpm.sock",
                "broken-scriptfilename" => "enable"
                ))
        )


We'll want to enable the following otherwise we'll get 403-Forbidden errors from the webserver:

        sudo lighttpd-enable-mod fastcgi fastcgi-php
        sudo service lighttpd force-reload




##Install MediaWiki
Installing and configuring the newest version of MediaWiki:

        wget https://releases.wikimedia.org/mediawiki/1.26/mediawiki-1.26.0.tar.gz
Extract the archive:        

        tar xvzf mediawiki-*.tar.gz
Create a new mediawiki directory in the webserver root and move the contexts of mediawiki to it:

        mkdir -p /var/www/mediawiki
        mv mediawiki-1.26.0/* /var/www/mediawiki
###Starting the Web Installation
On your local machine, we can now go to http://localhost/mediawiki and start the configuration using all of the installed components
![](http://i.imgur.com/Male16R.png)
Mediawiki will perform environmental checks to ensure that Mediawiki can be installed.
Upon connecting MySQL plug in the database information we created above.
![]()  <--screenshot
Click continue to select the default options InnoDB and Binary.
Next, name your wiki and create an admin account with a secure password of at least 8 characters.
We should go through the next optional as it concerns licenses and copyright as well as email settings.
Here is where you also have options for skins, extensions, and whether users may upload files or not.

The MediaWiki installation will automatically offer the download of a LocalSettings.php file.
Open up a local terminal so that there is one the local machine and one that is still currently connected via SSH to your server.
On the local machine cd to the directly where the LocalSettings.php file got downloaded to.
Next:
cat LocalSettings.php
and copy all of the text starting with **<?php**
Going back to the terminal that is connected to the server:

        nano /var/www/mediawiki/LocalSettings.php
        
Control-O to save the file and keep the file named LocalSettings.php
Once that file is saved, either click the **enter your wiki** link or enter the wiki by going to:
http://[public IP address]/mediawiki/index.php

##Securing your wiki with SSL
##Conclusion
We now have a secure MediaWiki with Lighttpd instance running on Ubuntu 14.04.
It's quickly installed and configured.
              by John Schriner
