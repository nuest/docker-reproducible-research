#  Getting started with Docker

10 Minutes

-------------------------

## Learning Objectives

* Start a container
* Understand difference between image and container
* Use Docker help on command line

----------------------------------------------------

## Start your first containers

Open a command line interface (CLI), sometimes also called "terminal" or "shell".

Then type in the following command:

```bash
$ docker run hello-world
```

That's it! You just ran a container on your computer.
In this case, your computer as the container's "host" maschine.
The container simply put out a message to the console.

Let's try out the suggested "more ambitious" command:

```bash
$ docker run -it ubuntu bash
```

In this case, you just started a container running the Ubuntu Linux distribution.

The Docker command we just use has four parts:

- `run` is Docker's instruction to create and start a container
- `-it` attached an `i`interactive `t`erminal - this way we can enter more commands and see their output
- `ubuntu` is the image name the container is based on
- `bash` is the command that is run inside the container, in this case the [Bourne Again Shell](https://en.wikipedia.org/wiki/Bash_(Unix_shell)), so you are in a CLI session within a container.

We can leave the container session with

```bash
root@46f5943a6c2e:/# exit
```

_How is this useful for reproducible computational research?_

The image was automatically downloaded from the default registry of images, the [Docker Hub](https://hub.docker.com).
You can also load images from local files or from an image registry hosted by other organisations.

The name `ubuntu` was automatically extended with the default tag `latest`.
_Tags_ are a mechanism to give names to variants of images.
For Ubuntu, there are tags for current and old releases of the operating system.
So for reproducibility, we should explicitly name the release we want.

```bash
# older OS
$ docker run -it ubuntu:10.04 bash
root@29fdfea48a9f:/# cat /etc/*release
exit

# newer OS
$ docker run -it ubuntu:17.04 bash
root@1a7f5a3619a8:/# cat /etc/*release
exit
```

Docker let's us work with outdated or new/unstable noperating system versions easily.

This can be extended to versions of software libraries and even particular combinations of libraries needed for a specific analysis, see e.g. [this paper](http://dx.doi.org/10.3390/rs9030290).

You can find out more on the [`run` command in the Docker docs](https://docs.docker.com/engine/reference/run/).

<!-- remove all exited containers: docker rm $(docker ps -q -f status=exited) -->

## Image vs. container

An image is a binary file encapsualating a complete "operating system".
When you tell the Docker engine to start a new container, the image is the blueprint for it.
You can run multiple containers from the same image.
A container can then be stopped and restarted again.
Since the container can change its own state while it is running (e.g. change a file) and diverge from its original state based on the image.
Whenever a file is changed within the container, a new copy of the file is created to not change the original one in the image (_"copy-on-write" strategy_).

You can learn more about [images, containers and storage in the Docker docs](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/).

_How is this useful for reproducible computational research?_

We can save and share both images and containers, so capture a specific state of the runtime environment that is independent from the host maschine.
For reproducibility, images are more interesting, since they are based on a human readable manifest for their contents, which we will introduce in a later section of this course.

## Managing local images

When you work with Docker a little while, you will download a variety of images.
These might capture disk space on your computer, so it is good to know how to manage them.

```bash
# list images
docker images

# remove image by name and tag
docker rmi ubuntu:10.04
```

You can learn more about the [`images` command in the Docker docs](https://docs.docker.com/engine/reference/commandline/images/).

## Managing local containers

You can run multiple containers in parallel, if you like.
To keep an eye on the resources they use, you can list and control them with the following commands.

```bash
docker ps

# list also the previously running containers, which are now stopped
docker ps -a

# remove a container, e.g. to re-use its name
docker rm <containerid or name>
```

## Docker CLI command completion and help

In this tutorial, we used only the command line to control Docker containers.
This is advantageous over using a graphical user interface, because you can include the commands in the scripts, and it is faster because you don't have to type the whole command and avoid typos.

Type `docker` into the terminal and double-press the `TAB` key.
You see a long list of available commands, only a few of which we will use in this course.

The online Docker documentation is extensive, and there are a vast number of tutorials on using Docker.
However, to use Docker effectively, it is best to get acquainted with the build-in help:
appending `--help` to any Docker command will list the available options and can answer usage questions in 80% of the cases.

Take a look at the help of commands we have already used.

```bash
docker run --help
docker images --help
docker rmi --help
docker ps --help

# get help on the commands with
docker --help
```

## The most important commands

 **Command** | **Explanation** 
 ----- | -----
`docker ps` | list all the running containers on the host
`docker ps -a` | list all the containers on the host, including those that have stopped
`docker exec -it <container-id> bash` | opens bash shell for a currently running container
`docker stop <container-id>` | stop a running container
`docker kill <container-id>` | force stop a running container
`docker rm <container-id>` | removes (deletes) a container
`docker rmi <container-id>` | removes (deletes) an image
`docker rm -f $(docker ps -a -q)` | remove _all_ current containers
`docker rmi -f $(docker images -q)` | remove _all_ images, even those not in use

[source](https://benmarwick.github.io/UW-eScience-docker-for-reproducible-research/#11)

## More information on Docker

Docker is not intended for reproducible research, but the intention of packaging an application with all its dependencies much overlap with reproduction of computations.

Docker has been called _"lightweight virtualization"_, but that requires an understanding of virtual machines.
A better image is the one of _houses vs. appartments_. With a house, you "own" and control everything, but in an apartment you only control what is inside your appartment, but have some shared infrastructure outside of your apartment.

In this lesson we're only using a fraction of what Docker offers, but it is woth exploring the [original use cases](https://www.doLearncker.com/what-docker) of Docker.
Try to learn some more on the large number of Docker commands using the build-in help of the CLI.

```bash
~$ docker <TAB TAB>
attach   cp       diff     export   images   inspect  login    network  ps       rename   rmi      search   stop     unpause  volume
build    create   events   help     import   kill     logout   pause    pull     restart  run      start    tag      update   wait
commit   daemon   exec     history  info     load     logs     port     push     rm       save     stats    top      version
```

<!--
Next: [Working with OpenRefine](01-working-with-openrefine.html)
-->