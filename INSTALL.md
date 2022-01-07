Luminance Installation
=========

Dependencies
------------
 - PHP >= 7.0
 - MySQL >= 5.6
 - Memcached
 - Nginx (recommended) or Apache
 - Sphinx 2.0.x
 - Radiance

PHP Modules
-----------
* php-mcrypt
* php-mbstring
* php-memcache
* php-mysqlnd
* php-dom
* php-xml

Composer
--------
cd into the Luminance directory and follow the brief instructions on https://getcomposer.org/download/ to download composer.

Once downloaded simply run the following command:
```
php composer.phar install
```

Database
--------
You need to create a database before running the Luminance install:
```
mysql -u root -p
CREATE DATABASE luminancedb;
CREATE USER 'luminance'@'localhost' IDENTIFIED BY '<password>';
GRANT ALL PRIVILEGES ON luminancedb. * TO 'luminance'@'localhost';

```
Ensure the database password is both stong and unique, preferably a random string.

Luminance
---------
To install a brand new instance of Luminance cd into the Luminance directory and run these commands:
```
php application/entry.php setup configure
php application/entry.php setup install

```

To upgrade an existing instance of Luminance cd into the Luminance directory and run this command:
```
php application/entry.php setup upgrade

```

To migrate from Gazelle cd into the Luminance directory and run these commands:
```
php application/entry.php setup configure ../../path/to/gazelle/classes/config.php
php application/entry.php setup upgrade

```

Sphinx
------
An example Sphinxsearch configuration file can be found in the install directory.

Nginx Configuration
-------------------
An example http and https Nginx vhost configuration files can be found in the install directory.

Cronjobs
--------
```
crontab -e

```
Set the following as contents for the file:
```
0,15,30,45  *  *   *    *       /usr/bin/php /var/www/localhost/application/entry.php schedule >> /root/schedule.log
*           *  *   *    *       /usr/bin/indexer -c /etc/sphinxsearch/sphinx.conf --rotate delta
5           *  *   *    *       /usr/bin/indexer -c /etc/sphinxsearch/sphinx.conf --rotate --all

```
