Docker base image: Nginx
=======================================

Base image prepared to use [Nginx](http://nginx.org) as recerse-proxy for [Puma](http://puma.io) rack-server prepared for deploy on [AWS Elasticbeanstalk](http://aws.amazon.com/ru/elasticbeanstalk/).

[![](https://badge.imagelayers.io/asux/nginx:latest.svg)](https://imagelayers.io/?images=asux/nginx:latest 'Get your own badge on imagelayers.io')

## Dockerfile

Dockerfile on [Github](https://github.com/asux/docker-images/blob/master/nginx/Dockerfile).

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

To push to [Docker Hub repo](https://hub.docker.com/r/asux/nginx/):

```shell
make push
```

Or do this all:

```shell
make
```
