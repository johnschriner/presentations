#How To Set Up the Latest MediaWiki with Lighttpd on Ubuntu 14.04

##Introduction

MediaWiki is a popular open source wiki platform that can be used for public or internal collaborative content publishing. MediaWiki is used for many of the most popular wikis on the internet including Wikipedia, the site that the project was originally designed to serve.

In this guide, we will be setting up the latest version of MediaWiki on an Ubuntu 14.04 server. We will use the Lighttpd web server to make the actual content available, php-fpm to handle dynamic processing, and mysql to store our wiki's data.
##Prerequisites


To complete this guide, you should have access to a clean Ubuntu 14.04 server instance. On this system, you should have a non-root user configured with sudo privileges for administrative tasks. You can learn how to set this up by following our [Ubuntu 14.04 initial server setup guide](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04).

When you are ready to continue, log into your server.  We will be connected through a terminal to our server via SSH.  More information on SSH can be found [here](https://www.digitalocean.com/community/tutorials/how-to-connect-to-your-droplet-with-ssh).  As we're going to be installing software, make sure you either enter the following and then your root password for administrator privileges or simply type sudo before each command in this tutorial:

        sudo su


It's good practice to make certain that your system is up to date with:

        sudo apt-get update
        sudo apt-get upgrade

##Install the Server Components
We will be setting up and configuring a **L**inux, **L**ighttpd, **M**ySQL, **P**HP (LLMP) stack.  We're installing each component separately.

###Installing Lighttpd
Lighttpd (pronounced *Lighty*) webserver is highly efficient, quick, and easy to install.
Install Lighttpd using apt-get:

        sudo apt-get install lighttpd
After installation, the web server will automatically start.  Point the browser on your local machine to your Droplet's public IP address and the placeholder page with show up at the default port `:80`.
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
Install the newest MySQL Server using apt-get:

        sudo apt-get install mysql-server
You will be asked to create a root password.  Make sure to remember it or place it in a password manager; we'll need the root password for setting up MediaWiki.

MySQL service will start automatically but to check that the service has opened a port you can try:

        nmap localhost

MySQL will have port 3306 opened.

<img src="http://i.imgur.com/wIfVYNb.png" alt="nmap shows us which ports are open" width="400">

 
MySQL is a service like Lighttpd and it can be administered from the command line:

        sudo service mysql start
        sudo service mysql stop                
        sudo service mysql restart

###Installing PHP-FPM        
Install PHP and FPM (FastCGI Process Manager) with:

        apt-get install php5-cli php5-cgi php5-mysql php5-fpm

PHP-FPM is an alternative to Lighttpd's spawn-fcgi PHP FastCGI implementation.  Essentially, with its adaptive process spawning it helps to handle traffic for busy sites.  We'll configure this further below.

After installation we can verify it was properly installed and get the version number:

        php -v

##Configure MySQL and Create Credentials for MediaWiki
Log into MySQL as root:

        mysql -u root -p
At the mysql prompt now, we do the following to create a user:

        CREATE DATABASE mediawikidb;
        CREATE USER mediawikiuser@localhost IDENTIFIED BY 'mediawikipassword';
        GRANT index, create, select, insert, update, delete, alter, lock tables on mediawikidb.* TO mediawikiuser@localhost;
        FLUSH PRIVILEGES;
        exit

##Configure Lighttpd and PHP-FPM

First, we need to enable PHP-FPM for Lighttpd.  To do this we'll need to uncomment the line `cgi.fix_pathinfo=1` in `/etc/php5/fpm/php.ini`:

        nano /etc/php5/fpm/php.ini
This is a very large file and this line is 768 in the _Paths and Directories_ section.  
The keyboard shortcut <kbd>ctrl</kbd> + <kbd>c</kbd> in nano shows the line number.

<img src="http://i.imgur.com/JNkP3iz.png" alt="uncommenting line 768" width="600">

        
We now need to configure Lighttpd to use PHP-FPM instead of its default spawn-fcgi.
To do this, `cd` to Lighttpd's configuration file directory:

        cd /etc/lighttpd/conf-available/
Then make a backup copy of `15-fastcgi-php.conf`:

        cp 15-fastcgi-php.conf 15-fastcgi-php-spawnfcgi.conf
Now, we'll edit the old `15-fastcgi-php.conf`:

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


We'll want to enable the modification and then reload Lighttpd:

        sudo lighttpd-enable-mod fastcgi fastcgi-php
        sudo service lighttpd force-reload

To test that PHP-FPM is now the FastCGI server, create `info.php` in the web root of the server:

        nano /var/www/info.php

Paste the following line into the file:

        <?php phpinfo(); ?>

Save the file as `info.php`

Direct the local web browser to `http://[SERVER_IP]/info.php` and see that FPM/FastCGI is now the server API.
<img src="http://i.imgur.com/hV1OKMb.png" alt="php5-fpm" width="300">


##Install MediaWiki
Installing and configuring the newest version of MediaWiki:

        cd /tmp
        wget https://releases.wikimedia.org/mediawiki/1.26/mediawiki-1.26.0.tar.gz
Extract the archive:        

        tar xvzf mediawiki-*.tar.gz
Create a new `mediawiki` directory in the webserver root and move the contexts of the extracted `mediawiki` directory to it:

        mkdir -p /var/www/mediawiki
        mv mediawiki-1.26.0/* /var/www/mediawiki
###Starting the Web Installation
On the local machine, go to `http://[SERVER_IP]/mediawiki` and start the configuration using all of the components we've installed.

<img src="http://i.imgur.com/Male16R.png" alt="starting mediawiki configuration" width="250">

MediaWiki will perform environmental checks to ensure that MediaWiki can be installed.

Enter in the database information we created [above](https://github.com/johnschriner/presentations/blob/master/digitalocean.md#configure-mysql-and-create-credentials-for-mediawiki).

<img src="http://i.imgur.com/NFvz9vF.png" alt="MySQL credentials" width="250">

Click _continue_ to select the default options `InnoDB` and `Binary`.

Next, name the wiki and create an admin account with a secure password of at least 8 characters.  Remember this username and password for administration once MediaWiki is installed.

We should go through the next optional page as it concerns licenses, copyright, and email settings.
Here is where you also have options for skins, extensions, and whether or not users may upload files.

The MediaWiki installation will automatically offer the download of a `LocalSettings.php` file.  Save the file locally.

<img src="http://i.imgur.com/9zju96B.png" alt="download LocalSettings.php" width="500">

Open up a local terminal so that there is one for the local machine and one that is still currently connected via SSH to your server.
On the local machine, `cd` to the directory where the `LocalSettings.php` file was downloaded to.

Next:

        cat LocalSettings.php
        
Copy all of the text from that file starting with **<?php**

Going back to the terminal that is connected via SSH to the server:

        nano /var/www/mediawiki/LocalSettings.php
        
Paste all of the text, press the shortcut <kbd>ctrl</kbd> + <kbd>o</kbd> to save the file and keep the file named `LocalSettings.php`.

This file can be edited to change the name of the MediaWiki or edit many of the configurations from our web setup.
Once that file is saved, either click the _enter your wiki_ link or enter the wiki by going to `http://[SERVER_IP]/mediawiki/index.php`

##A Note on Adding Extensions and an Example
MediaWiki's [_Get Extensions_](https://www.mediawiki.org/wiki/Category:Extensions) page showcases hundreds of extensions to add to MediaWiki.  

Generally, extensions go in their own subdirectory at `http://[SERVER_IP]/mediawiki/extensions/`.

Before installing extensions, make certain that there is still active development of the extension and that you've read the documentation.

Many of these extensions can be setup by moving a directory into '/var/www/mediawiki/extensions/' and simply editing _LocalSettings.php_.

The [Maintenance](https://www.mediawiki.org/wiki/Extension:Maintenance) extension is a useful set of scripts for many tasks including cleaning up spam, checking usernames, and checking bad redirects.

Go to the extension's download page:

        https://www.mediawiki.org/wiki/Extension:Maintenance
        
Click 'Download snapshot' and select 'MediaWiki version 1.26'.  Click 'Continue'.

Instead of downloading the file to the local machine, click `cancel` on the download dialog and we see that MediaWiki has a snapshot URL for the extension's tar.gz file.
In the ssh session with the Droplet:

        cd /tmp
        wget [the complete URL for the tar.gz file]
        tar -xzf [the tar.gz file] -C /var/www/mediawiki/extensions/

The latest snapshot for the extension is now in the extensions directory.

Lastly, for extensions we'll need to edit the `LocalSettings.php` file:

        nano /var/www/mediawiki/LocalSettings.php
Add the following line to the bottom of of the file in the `more configuration options` section:

        require_once "$IP/extensions/Maintenance/Maintenance.php";

After that line, add the following line to grant permission to sysop and maintenance groups to access the special page and run maintenance scripts:

        $wgGroupPermissions['sysop']['maintenance'] = true;
        
The very last lines of `LocalSettings.php` should now look like this:

<img src="http://i.imgur.com/FMQmV8G.png" alt="Adding extensions" width="400">



Save the file with <kbd>ctrl</kbd> + <kbd>o</kbd>, then <kbd>enter</kbd>, and <kbd>ctrl</kbd> + <kbd>x</kbd> to exit out.

To check that the extension installed properly, navigate in the left column to:
`Special Pages: Data and Tools: Version`, or enter in the URL:

        http://[SERVER_IP]/mediawiki/index.php?title=Special:Version

In the `Installed Extensions` section, Maintenance extension will be listed, no restart of the services necessary.

By clicking on the link for `Wiki Interface` or navigating to:

`http://[SERVER_IP]/mediawiki/index.php?title=Special:Maintenance`, we'll see all of the maintenance scripts available.


##Conclusion
We now have the latest MediaWiki with Lighttpd running on Ubuntu 14.04.

We've added a useful extension using the typical method.  Now we have to start creating content.
<p align="right">by John Schriner</p> 

