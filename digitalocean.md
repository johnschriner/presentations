#How To Set Up the Latest MediaWiki with Lighttpd on Ubuntu 14.04

##Introduction

MediaWiki is a popular open source wiki platform that can be used for public or internal collaborative content publishing. MediaWiki is used for many of the most popular wikis on the internet including Wikipedia, the site that the project was originally designed to serve.

In this guide, we will be setting up the latest version of MediaWiki on an Ubuntu 14.04 server. We will use the lighttpd web server to make the actual content available, php-fpm to handle dynamic processing, and mysql to store our wiki's data.
##Prerequisites


To complete this guide, you should have access to a clean Ubuntu 14.04 server instance. On this system, you should have a non-root user configured with sudo privileges for administrative tasks. You can learn how to set this up by following our Ubuntu 14.04 initial server setup guide.

When you are ready to continue, log into your server.  As we're going to be installing software, make sure you either enter the following and then your root password for administrator privileges or simply type sudo before each command in this tutorial:

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

##Installing and Configure MySQL and Create Credentials for MediaWiki
Next, we'll install and configure MySQL database to store the information for the wiki.
Install the newest MySQL using apt-get:

        sudo apt-get install mysql-server

##Create Credentials for MediaWiki
##Configure PHP-FPM and Lighttpd
##Install MediaWiki
##Conclusion
We now have a secure MediaWiki with Lighttpd instance running on Ubuntu 14.04.
It's quickly installed and configured.
              by John Schriner
