# Running a local Docker Registry

If you give a course on Docker, and 30 people run the same Docker pull command at the same time, it is a challenge for even the best university networks to handle. Therefore it could be useful to run a local Docker registry. It certainly adds some complexity in the beginning, but is very useful for courses using domain specific images (and not just `hello-world`).

## Resources

- https://docs.docker.com/registry/recipes/mirror/#what-if-the-content-changes-on-the-hub (run the registry as a pull-through cache)
- https://docs.docker.com/registry/insecure/ (running a self-signed or insecure registry, the former should be fine for most courses)
- https://rominirani.com/docker-tutorial-series-part-6-docker-private-registry-15d1fd899255

## Setting up the registry as a plain HTTP registry

```bash
cd registry
docker-compose up
```

Ask the course participants to follow the instructions here:

https://docs.docker.com/registry/insecure/#deploying-a-plain-http-registry

to add your local computer's IP and the respective port to the list of insecure registries, e.g.

```json
{
  "insecure-registries" : ["my-laptop:5000","1.2.3.4:5000"]
}
```

Don't forget to restart the Docker daemon afterwards (`sudo service docker restart`, or the equivalent on the respective platform).

You can browse a list of available images at **http://[my-laptop]:5000/v2/_catalog**.

For **Docker toolbox**:

Create a new machine with `docker-machine` which enables the insecure registry and enable it.

```bash
docker-machine create --driver virtualbox --engine-insecure-registry my-laptop:5000 authorcarpentry
eval $(docker-machine env authorcarpentry)
```

Alternatively, try the solution [suggested here](https://github.com/docker/docker-registry/issues/1005#issuecomment-154815402) to update an existing machine.
Adjust this line in `/var/lib/boot2docker/profile` in the VirtualBox machine:

```
--insecure-registry <the hostname or IP, e.g. 192.168.99.100>:5000
```

## Adding images

You can now "fill" the registry by pulling images. This will add a few GB to your local disc!

**Important:** Run these commands by using the IP or hostname that the students will also use - it makes instructions much clearer!

### Popular images in Docker Hub

```
docker pull [my-laptop]:5000/library/alpine
docker pull [my-laptop]:5000/library/busybox
docker pull [my-laptop]:5000/library/centos
docker pull [my-laptop]:5000/library/centos:6
docker pull [my-laptop]:5000/library/debian
docker pull [my-laptop]:5000/library/debian:jessie
docker pull [my-laptop]:5000/library/debian:stretch
docker pull [my-laptop]:5000/library/debian:wheezy
docker pull [my-laptop]:5000/library/hello-world
docker pull [my-laptop]:5000/library/httpd
docker pull [my-laptop]:5000/library/httpd:alpine
docker pull [my-laptop]:5000/library/mariadb
docker pull [my-laptop]:5000/library/mariadb:5
docker pull [my-laptop]:5000/library/mongo
docker pull [my-laptop]:5000/library/mysql
docker pull [my-laptop]:5000/library/nginx
docker pull [my-laptop]:5000/library/nginx:alpine
docker pull [my-laptop]:5000/library/owncloud
docker pull [my-laptop]:5000/library/postgres
docker pull [my-laptop]:5000/library/postgres:alpine
docker pull [my-laptop]:5000/library/python
docker pull [my-laptop]:5000/library/python:2
docker pull [my-laptop]:5000/library/python:2-alpine
docker pull [my-laptop]:5000/library/python:alpine
docker pull [my-laptop]:5000/library/python:slim
docker pull [my-laptop]:5000/library/redis
docker pull [my-laptop]:5000/library/ubuntu
docker pull [my-laptop]:5000/library/ubuntu:14.04
docker pull [my-laptop]:5000/library/ubuntu:17.04
docker pull [my-laptop]:5000/library/ubuntu:trusty
docker pull [my-laptop]:5000/library/ubuntu:xenial
docker pull [my-laptop]:5000/library/ubuntu:zesty
docker pull [my-laptop]:5000/library/wordpress
docker pull [my-laptop]:5000/ubuntu
```

### R Images

```bash
# Rocker
docker pull [my-laptop]:5000/rocker/r-ver
docker pull [my-laptop]:5000/rocker/r-ver:3.1.0
docker pull [my-laptop]:5000/rocker/r-ver:3.3.0
docker pull [my-laptop]:5000/rocker/r-ver:3.3.1
docker pull [my-laptop]:5000/rocker/r-ver:3.3.3
docker pull [my-laptop]:5000/rocker/r-ver:3.4.1
docker pull [my-laptop]:5000/rocker/r-ver:devel
docker pull [my-laptop]:5000/rocker/rstudio
docker pull [my-laptop]:5000/rocker/rstudio:3.4.1
docker pull [my-laptop]:5000/rocker/rstudio:devel
docker pull [my-laptop]:5000/rocker/tidyverse
docker pull [my-laptop]:5000/rocker/tidyverse:3.4.1
docker pull [my-laptop]:5000/rocker/verse
docker pull [my-laptop]:5000/rocker/verse:3.4.1
docker pull [my-laptop]:5000/rocker/verse:3.4.1
docker pull [my-laptop]:5000/rocker/geospatial:3.4.1

# MRO and Renjin
docker pull [my-laptop]:5000/nuest/mro
docker pull [my-laptop]:5000/nuest/mro:3.4.1
docker pull [my-laptop]:5000/nuest/renjin
```

### Geospatial images

Based on list [https://wiki.osgeo.org/wiki/DockerImages](https://wiki.osgeo.org/wiki/DockerImages).

```bash
rocker/geospatial

kartoza/postgis
# https://github.com/kartoza/docker-qgis-desktop#example-use-with-docker-compose
kartoza/qgis-desktop
kartoza/qgis-desktop:2.18
kartoza/qgis-desktop:2.14
kartoza/qgis-desktop:2.12
kartoza/qgis-desktop:2.10
# https://github.com/kartoza/docker-qgis-server#example-use-with-docker-compose
kartoza/qgis-server
kartoza/qgis-server:2.18
kartoza/qgis-server:2.14
kartoza/qgis-server:LTR

# https://github.com/geo-data/gdal-docker
geodata/gdal
# https://github.com/geo-data/grass-docker
docker run geodata/grass --help
# 
geodata/mapserver

# https://github.com/sverhoeven/docker-cartodb#how-to-run-the-container (full stack!)
sverhoeven/cartodb

# https://github.com/geonetwork/docker-geonetwork and https://hub.docker.com/_/geonetwork/
library/geonetwork
library/geonetwork:postgres

geocontainers/pycsw
geocontainers/52n-wps

# https://github.com/DCAL12/docker-python-geospatial
dcal12/python-geospatial
```

### Maintenance

Check the size with `du -hs /tmp/local-docker-registry/docker/registry/v2/*` (leave out the `s` to get each directory).

You can clear your client registry of all these images afterwards with

```
docker images | grep localhost:5000 | awk '{print $3}' | xargs docker rmi --force
```

### Pushing specific imags manually

```bash
docker tag my-paper gin-nuest:5000/demo/my-paper
docker push gin-nuest:5000/demo/my-paper
```

## [WIP] Setting up the registry with a self-signed certificate

```bash
$ openssl req -newkey rsa:4096 -nodes -sha256 -keyout certs/domain.key -x509 -days 365 -out certs/domain.crt
```

When asked for "Common Name (e.g. server FQDN or YOUR name)", put in _your IP in the local network_, because `localhost` will only work for your own machine.
Alternatively, run the following command, which has the data normally queried interactively already included ([via](https://raymii.org/s/snippets/OpenSSL_generate_CSR_non-interactivemd.html)). It uses a [two](https://security.stackexchange.com/a/159537) [tricks](https://askubuntu.com/a/604691/493585) to get your current IP and add it, besides localhost, to the certificate.

```
MY_IP=$(ip route get 8.8.8.8 | awk '{print $NF; exit}')
openssl req -newkey rsa:4096 -nodes -sha256 -keyout certs/domain.key -x509 -days 365 -batch -subj "/C=DE/ST=Ocean/L=Whale City/O=Docker for RR/OU=Author Carpentry/CN=$(hostname)" -reqexts SAN -config <(cat /etc/ssl/openssl.cnf <(printf "[SAN]\nsubjectAltName=DNS:$MY_IP,DNS:localhost")) -out certs/domain.crt
```

Note the SHA-256 Fingerprint and tell it to the group if they want to be sure.

**https://localhost:5000/v2/_catalog**

## Setting up registry UI

https://github.com/kwk/docker-registry-frontend

https://github.com/Joxit/docker-registry-ui

## Setting up nginx proxy

only allow specific IPs (local network) to access the registry

could re-use the UI's nginx?
