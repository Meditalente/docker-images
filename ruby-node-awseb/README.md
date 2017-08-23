Docker base image: Ruby + Node + AWS EB CLI
=========================================================================

Docker base image for [Ruby](https://ruby-lang.org) with [Node](https://nodejs.org) and prepared for deploy on [AWS Elasticbeanstalk](http://aws.amazon.com/ru/elasticbeanstalk/) based on [starefossen/ruby-node](https://hub.docker.com/r/starefossen/ruby-node/).

[![](https://badge.imagelayers.io/asux/ruby-node-awseb:latest.svg)](https://imagelayers.io/?images=asux/ruby-node-awseb:latest 'Get your own badge on imagelayers.io')

Dockerfile
----------

Dockerfile on [Github](https://github.com/asux/docker-images/blob/master/ruby-node-awseb/Dockerfile).

Build
------

Commmit changes and create new tag.

To build base image use:

```shell
make build
```

To tag latest image:

```shell
make tag_latest
```

To push to [Docker Hub repo](https://hub.docker.com/r/asux/ruby-node-awseb/):

```shell
make push
```

Or do this all:

```shell
make
```

Usage
-----

This image made for AWS EB multicontainer environment and assumes:

* The code mounts to `/usr/src/app`.
* The startup script `bin/start.sh` prepares and runs web service or worker service if `WORKER=true`.
