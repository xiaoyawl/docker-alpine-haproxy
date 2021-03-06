# HAProxy Alpine Linux image

[![](https://badge.imagelayers.io/janeczku/alpine-haproxy:1.5.svg)](https://imagelayers.io/?images=janeczku/alpine-haproxy:1.5 'Get your own badge on imagelayers.io') [![Docker Pulls](https://img.shields.io/docker/pulls/janeczku/alpine-haproxy.svg)](https://hub.docker.com/r/janeczku/alpine-haproxy/)

A micro-image providing HAProxy based on [Alpine Linux](https://hub.docker.com/_/alpine/). 90% smaller than the official HAProxy docker image.

[Github source](https://github.com/janeczku/docker-alpine-haproxy)

## Supported tags

-	`1.5.14`, `1.5`
-	`1.6.3`, `1.6`, `latest`
-	`1.6.3-lua`, `1.6-lua` *supports HAProxy [Lua scripting](http://blog.haproxy.com/2015/03/12/haproxy-1-6-dev1-and-lua/)*

## What is HAProxy?

HAProxy is a free, open source high availability solution, providing load balancing and proxying for TCP and HTTP-based applications by spreading requests across multiple servers. It is written in C and has a reputation for being fast and efficient (in terms of processor and memory usage).

> [wikipedia.org/wiki/HAProxy](https://en.wikipedia.org/wiki/HAProxy)

## How to use this image

Since no two users of HAProxy are likely to configure it exactly alike, this image does not come with any default configuration.

Please refer to [upstream's excellent (and comprehensive) documentation](https://cbonte.github.io/haproxy-dconv/) on the subject of configuring HAProxy for your needs.

It is also worth checking out the [`examples/` directory from upstream](http://www.haproxy.org/git?p=haproxy-1.5.git;a=tree;f=examples).

Note: Many configuration examples propose to put `daemon` into the `global` section to run HAProxy as daemon. Do **not** configure this or the Docker container will exit immediately after launching because the HAProxy process would go into the background.

## Create a `Dockerfile`

```dockerfile
FROM janeczku/alpine-haproxy:1.6
COPY haproxy.cfg /etc/haproxy/haproxy.cfg
```

Build and run:

```console
$ docker build -t my-haproxy .
$ docker run -d --name my-running-haproxy my-haproxy
```

## Directly via bind mount

```console
$ docker run -d --name my-running-haproxy -v /path/to/haproxy.cfg:/etc/haproxy/haproxy.cfg:ro janeczku/alpine-haproxy:1.6
```
