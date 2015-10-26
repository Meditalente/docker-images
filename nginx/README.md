Docker base image: Nginx
=======================================

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

To push to [Docker Hub repo](https://hub.docker.com/u/asux/nginx/):

```shell
make push
```

Or do this all:

```shell
make
```
