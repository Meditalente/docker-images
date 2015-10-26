Docker base image: Rails + Puma + PhantomJS
=======================================

Docker base image for [Rails](http://rubyonrails.org) runned with [Puma](http://puma.io) and [PhantomJS](http://phantomjs.org) 2.0.0 prepared for deploy on [AWS Elasticbeanstalk](http://aws.amazon.com/ru/elasticbeanstalk/).

[![](https://badge.imagelayers.io/asux/rails-phantomjs:latest.svg)](https://imagelayers.io/?images=asux/rails-phantomjs:latest 'Get your own badge on imagelayers.io')

## Dockerfile

Dockerfile on [Github](https://github.com/noplanb/rails-base/blob/master/Dockerfile).

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

To push to [Docker Hub repo](https://registry.hub.docker.com/u/zazo/rails/):

```shell
make push
```

Or do this all:

```shell
make
```

## Usage

Simple `Dockerfile` for your rails app is [here](https://github.com/noplanb/rails-base/blob/master/examples/Dockerfile).

Simple `Dockerrun.aws.json` is [here](https://github.com/noplanb/rails-base/blob/master/examples/Dockerrun.aws.json).

Simple EB config file with `rake db:migrate` is [here](https://github.com/noplanb/rails-base/blob/master/examples/eb.config).
