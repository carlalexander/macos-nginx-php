# Nginx configuration for Mac OS X as well as MySQL and MongoDB.

## Introduction
   
This is a nginx configuration for various PHP projects.

It is inspired by the work of [perusio](https://github.com/perusio "perusio") and [rellimevad](https://github.com/rellimevad "rellimevad"). Installation instructions initially found [here](http://www.rabblemedia.net/installing-nginx-php-fpm-and-mysql-drupal-osx-lion-homebrew "here").

## Supported projects

*  WordPress
*  Symfony 2

## Requirements

*  Mac OS X Lion
*  XCode
*  [Homebrew](http://mxcl.github.com/homebrew/ "Homebrew")
*  Git

## Installation

This will describe all the steps required to install everything. All of this is done through Terminal.

### MySQL

Installation steps.

	brew install mysql

	unset TMPDIR

	mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql --tmpdir=/tmp

	mysql.server start

Finally, MySQL is configured using this command:

	/usr/local/Cellar/mysql/5.5.20/bin/mysql_secure_installation

### PHP with php-fpm

#### Basic

There is no formula by default for PHP so we need to go get it.

	curl -O https://raw.github.com/ampt/homebrew-php/master/Formula/php.rb

	mv php.rb `brew --prefix`/Library/Formula

We can then install PHP using Homebrew.

	brew install php --with-mysql --with-fpm

#### mongo-php

	brew install https://github.com/josegonzalez/homebrew-php/raw/master/Formula/mongo-php.rb

#### xdebug

	brew install https://github.com/josegonzalez/homebrew-php/raw/master/Formula/php-xdebug.rb

### Nginx

First, install Nginx.

	brew install nginx

Importing our configuration requires us to replace the old config files. And cloning the git repo.

