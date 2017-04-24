#  Transfering and archiving Docker containers

10 Minutes

---------------------------------------------------
## Learning Objectives

* Save an image and export a container
* Add metadata to containers and images
* Upload to Zenodo

----------------------------------------------------

## Recap: Image vs. container

An image is a blueprint for a container.
A container is an instance of an image.
A container can divert from the image during its lifetime.

## Save a Docker image

```bash
docker save --output articles-wordcloud.tar authorcarpentry-docker-articles
ls *.tar
```

We use the `--output` option to save the image to a file.

You can learn more about the [`save` command on Docker Docs](https://docs.docker.com/engine/reference/commandline/save/).

_What does this mean for reproducible research?_

Images are nice because there is a dual relationship between the Dockerfile used to build the image and the image itself.
However, it requires additional work to create a matching image when you work _inside_ the container.

## Export a container

If you choose to manually manipulate a container, or include results of some processing, then you will export a container.

```bash
# find out the container ID
docker ps -a

docker save --output articles-wordcloud.tar authorcarpentry-docker-articles
ls *.tar
tar -tvf articles-wordcloud.tar
```

You can learn more about the [`export` command on Docker Docs](https://docs.docker.com/engine/reference/commandline/export/).

_What does this mean for reproducible research?_

You should be careful when exporting containers, because you lack the metadata/documentation of the Dockerfile.

## Labels for images and containers

Docker provides _labels_ to add custom metadata to images and containers.
You can use it to provide information that helps you and others to 

We can add labels to images by using the `LABEL` instructions in the Dockerfile.

```Dockerfile
FROM rocker/rstudio

LABEL name=my_image_for_research \
    author=Daniel
```

We can add labels when starting a container.

```bash
$ docker run -it --label experiment_run_numer=42 authorcarpentry-docker-articles

# find out container name
docker ps -a

# print out the label using inspect
docker inspect jolly_euclid | grep experiment
```

These labels will still be there after exporting and importing.

You can learn more about [labelling and custom metadata in the Docker docs](https://docs.docker.com/engine/userguide/labels-custom-metadata/) and about the [`inspect` command](https://docs.docker.com/engine/reference/commandline/inspect).

## Archiving a Docker image or container

You can now upload the [tarball](https://en.wikipedia.org/wiki/Tar_(computing)) to a data repository, such as [figshare](http://figshare.com/) or [Zenodo](http://zenodo.org/), get a [DOI](https://en.wikipedia.org/wiki/Digital_object_identifier) and cite it in your work.

<!--
## Loading and importing images and containers

...
-->

<!--
Previous: [Scripts](02-scripts.html) Optional Next: [Services in OpenRefine](04-services.html)
-->