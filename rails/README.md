Docker base image: Rails + Puma
=======================================

Docker base image for [Rails](http://rubyonrails.org) runned with [Puma](http://puma.io)
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

This image made for AWS EB multicontainer environment and assumes:
  * The [nginx](https://github.com/asux/docker-images/blob/master/nginx/) links this service as **web**.
  * The code mounts to `/usr/src/app`.
  * The startup script `bin/start.sh` prepares and runs web service or worker service if `WORKER=true`.

Example files you can find in [examples](https://github.com/asux/docker-images/blob/master/rails/examples/) folder.
