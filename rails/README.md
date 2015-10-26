Docker base image: Rails + Puma
=======================================

Docker base image for [Rails](http://rubyonrails.org) runned with [Puma](http://puma.io) prepared for deploy on [AWS Elasticbeanstalk](http://aws.amazon.com/ru/elasticbeanstalk/).

[![](https://badge.imagelayers.io/asux/rails:latest.svg)](https://imagelayers.io/?images=asux/rails:latest 'Get your own badge on imagelayers.io')

## Dockerfile

Dockerfile on [Github](https://github.com/asux/docker-images/blob/master/rails/Dockerfile).

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

To push to [Docker Hub repo](https://hub.docker.com/r/asux/rails/):

```shell
make push
```

Or do this all:

```shell
make
```

## Usage

Simple `Dockerfile` for your rails app is [here](https://github.com/asux/docker-images/blob/master/rails/examples/Dockerfile).

Simple `Dockerrun.aws.json` is [here](https://github.com/asux/docker-images/blob/master/rails/examples/Dockerrun.aws.json).
