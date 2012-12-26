# Nginx configuration for Mac OS X PHP Projects using MySQL and MongoDB.

## Introduction
   
This is a nginx configuration for various PHP projects.

It is inspired by the work of [perusio](https://github.com/perusio "perusio") and [rellimevad](https://github.com/rellimevad "rellimevad"). Installation instructions initially found [here](http://www.rabblemedia.net/installing-nginx-php-fpm-and-mysql-drupal-osx-lion-homebrew "here").

## Supported projects

*  WordPress (currently does not support wp-supercache)
*  Symfony 2

## Requirements

*  Mac OS X Lion
*  XCode
*  [Homebrew](http://mxcl.github.com/homebrew/ "Homebrew")
*  Git

## Installation

This will describe all the steps required to install everything. All of this is done through Terminal.

### Databases

#### MySQL

Installation steps.

	brew install mysql

	unset TMPDIR

	mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql --tmpdir=/tmp

	mysql.server start

Finally, MySQL is configured using this command:

	/usr/local/Cellar/mysql/5.5.20/bin/mysql_secure_installation

#### MongoDB

	brew install mongodb
	
#### PostgreSQL
	
	brew install postgresql
	
For new installations, You need to initialize the database:

	initdb /usr/local/var/postgres -E utf8

### PHP and other libraries

This step will explain how to install PHP with fpm as well as other libraies you might need for your projects.

_Please note that additional configuration options will be supplied by the homebrew installer. Please follow those directions._

#### PHP with Homebrew

There is no formula by default, but there is a github project maintainging all php brews. You can find it [here](https://github.com/josegonzalez/homebrew-php "here").

#### PHP with fpm

You can omit the `--with-mysql --with-pgsql` if you will not be using it.

	brew install php54 --with-mysql --with-pgsql --with-fpm

#### APC
	
	brew install php54-apc

#### mongo-php

	brew install php54-mongo

#### xdebug

	brew install php54-xdebug

### Nginx

First, install Nginx.

	brew install nginx

#### Configuration

Importing our configuration requires us to replace the old config files. And cloning the git repo.

1. Rename the default config directiory

	mv /usr/local/etc/nginx /usr/local/etc/nginx.old

2. Clone the git repository from github. _Or, alternatively, you can also download the files and copy the manually._

3. Use the default configs in `sites-available` to create your site configs.

4. Create a `sites-enabled` directory.

	mkdir /usr/local/etc/nginx/sites-enabled

5. Create symlinks to your config files in `sites-available` in `site-enabled` using `ln -s`.

## Project Configuration

### Nginx User

By default, the user is `nobody`.

### WordPress

You'll need to give write access to your WordPress folder to the nginx user. You'll also need to give ownership to the files to the nginx user if you want the automatic updates to work. This is done using `chown -R nobody /path/to/wp`. If you're using a different user, replace `nobody` by that user.
