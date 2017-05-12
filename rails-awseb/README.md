Docker base image: Rails + Puma + AWS EB CLI
=======================================

Docker base image for [Rails](http://rubyonrails.org) runned with [Puma](http://puma.io) prepared for deploy on [AWS Elasticbeanstalk](http://aws.amazon.com/ru/elasticbeanstalk/).

[![](https://badge.imagelayers.io/asux/rails-awseb:latest.svg)](https://imagelayers.io/?images=asux/rails-awseb:latest 'Get your own badge on imagelayers.io')

## Dockerfile

Dockerfile on [Github](https://github.com/asux/docker-images/blob/master/rails-awseb/Dockerfile).

## Build
Commmit changes and create new tag.

To build base image use:

```shell
make build
```

To tag latest image:

```shell
make tag_latest
```

To push to [Docker Hub repo](https://hub.docker.com/r/asux/rails-awseb/):

```shell
make push
```

Or do this all:

```shell
make
```

## Usage

This image made for AWS EB multicontainer environment and assumes:
  * The [nginx](https://github.com/asux/docker-images/blob/master/nginx/) links this service as **web**.
  * The code mounts to `/usr/src/app`.
  * The startup script `bin/start.sh` prepares and runs web service or worker service if `WORKER=true`.

Example files you can find in [examples](https://github.com/asux/docker-images/blob/master/rails-awseb/examples/) folder.
