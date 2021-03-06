Skeleton Service
===================

This project is intented to be a skeleton for PHP based services.

[![Minimum PHP Version](http://img.shields.io/badge/php-%3E%3D%205.4-8892BF.svg)](https://php.net/)
[![Build Status](https://travis-ci.org/CrakLabs/skeleton-service.svg)](https://travis-ci.org/CrakLabs/rest-normalizer)
[![SensioLabs Insight](https://img.shields.io/sensiolabs/i/16996788-c5c9-4f59-817e-23592755f98d.svg)](https://insight.sensiolabs.com/projects/16996788-c5c9-4f59-817e-23592755f98d)
[![License](https://img.shields.io/packagist/l/craklabs/skeleton-service.svg)](https://packagist.org/packages/craklabs/skeleton-service)

Getting started
===================

    $ docker build -t crakmedia/skeleton-service:latest .
    
    $ cp docker-compose.yml.dist docker-compose.yml

    $ docker-compose run shell

        $ composer install

    $ docker-compose up


Overriding default settings
==================

Should over need to override the default configuratio for any of the services
runing within the container, you can add docker volumes to your docker-compose.yml.
As an example, say you need to modify the default nginx configuration provided by
the base image. In this case you just need to add a new voluming mapping under the
volumes section in your docker-compose.yml file:


    volumes:
     ... existing mappings ...
     - /path/to/nginx.conf:/etc/nginx/nginx.conf

The following is a list of files/directories added in the base image, which could be
overriden:
  
    - /etc/nginx/conf.d
    - /etc/nginx/nginx.conf
    - /etc/php.ini
    - /etc/php-fpm.conf
    - /etc/php-fpm.d

Of course you can always use docker volumes to override any file/directory within a running
container. See [here](https://docs.docker.com/userguide/dockervolumes/) for more details.

Migrations
==================

Run migrations

    $ docker-compose run shell

    $ php app/console migrations:migrate

Tests
==================

First, go in your container shell

    $ docker-compose run shell

Copy `tests/config.yml.dist` to `tests/config.yml` and configure your test database

    $ cp tests/config.yml.dist tests/config.yml

Functional tests

    $ bin/behat

Generate doc
==================

Install apidoc

    $ npm install apidoc -g

Generate doc

    $ apidoc -i src/Controller/ -o doc

Launch `doc/index.html` with your browser.


Monitor your metrics
==================

In order to monitor metrics of application, you should use $app['monitor']. For more information about how to use, see
[documentation of the client](https://github.com/thephpleague/statsd)
