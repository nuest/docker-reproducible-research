#  Jupyter in Docker container

10 Minutes


---------------------------------------------------

## Learning Objectives

* User Jupyter Notebook started in a Docker container
* Share a local directory with running container for data import and export

----------------------------------------------------

## Start container

Many different Docker images exist for [Python](https://hub.docker.com/search/?isAutomated=0&isOfficial=0&page=1&pullCount=0&q=python&starCount=0).
In this lesson, we'll try out a [Jupyter](https://jupyter.org/) image.

> The Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations and explanatory text. Uses include: data cleaning and transformation, numerical simulation, statistical modeling, machine learning and much more. _https://jupyter.org/_

Jupyter images are available as different ["opinioned ready-to-run stacks"](https://github.com/jupyter/docker-stacks).

```bash
docker run -it --rm -p 8888:8888 jupyter/scipy-notebook:eb70bcf1a292
# stop the container with Ctrl+c
```

In this case we use a new CLI option, `--rm` to remove the container right-away after it is closed
Some housekeeping on container instances never hurts!
We also use a specific [release tag](https://hub.docker.com/r/jupyter/scipy-notebook/tags/) so we are reproducible.

Open your browser at the URL provided in the console, e.g. `http://localhost:8888/?token=fce55...<token string>`, create a new notebook and start editing your Python code, or copy and paste an example from the [Numpy tutorial](https://cs231n.github.io/python-numpy-tutorial/) or from [Matplotlib](http://matplotlib.org/gallery.html) gallery.

## Mount a directory from the host

To use files from your host computer and make data available in a container, you can mount volumes.
This means you create a link between a directory on the host and a directory in the container.
You can preserve work when containers are deleted, or between containers.

This part of the lesson is based on the Data Carpentry course [_Python for ecologists: starting with data_](http://www.datacarpentry.org/python-ecology-lesson/01-starting-with-data/).

```bash
# download a data file
mkdir /tmp/author-carpentry-docker
cd /tmp/authorcarpentry-docker
wget -O lc-articles.zip https://ndownloader.figshare.com/files/5330251
unzip lc-articles.zip

# mount a volume when starting the container
docker run -it --rm -p 8888:8888 -v /tmp/authorcarpentry-docker:/home/jovyan/work:rw jupyter/scipy-notebook:eb70bcf1a292
```

We use the `:rw` option, meaning we allow `r`eading and `w`writing from within the container, as oppossed to `ro` (read-only).

Learn more about [volume mounts in the Docker docs](https://docs.docker.com/engine/tutorials/dockervolumes/#data-volumes).

We can now load the mounted data in the notebook:

```Python
import pandas as pd
pd.read_csv("articles.csv")
```

_How is this useful for reproducible research?_

It is not, because we separate the data from the container, which is not self-consistent anymore.
But mounting host volumes is useful for data input and output during development, and also for large datasets, which cannot easily be replicated multiple times on the same machine.

## Next steps

If you have not used Jupyter notebooks before, but use Python scripts for your work, then you can of course also wrap a Python script and its dependencies in a container.
There are a number of Python images available on the Docker Hub that can get you started.
You can even make your script the containers default command and provide instructions to your script when running a container.

- [Blog post on RR with Anaconda](https://www.continuum.io/blog/developer-blog/anaconda-and-docker-better-together-reproducible-data-science)
- ...

<!--
Previous: [Working with OpenRefine](01-working-with-openrefine.html)  Next: [Saving and Exporting files and projects](03-save-export.html)
-->