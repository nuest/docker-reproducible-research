# Templates for reproducible research

15 Minutes

---------------------------------------------------

## Learning Objectives

- What are Dockerfiles?

---------------------------------------------------

## Writing a Dockerfile

Docker can build images based on the instructions from a Dockerfile.
The instructions can be used for example to run arbitrary commands in the container and to copy files.
Images can extend on existing images.

Create a new text file named `Dockerfile` in a temporarly directory.

```bash
cd /tmp/authorcarpentry-docker/
touch Dockerfile
```

Open it with a text editor and paste the following content

```Dockerfile
FROM rocker/rstudio

WORKDIR /home/rstudio
COPY articles.csv articles.csv

RUN install2.r wordcloud tm
```

We use Rocker's RStudio as the base image and copy the file `articles.csv` into the container to the directory `/data`.

Now we must tell Docker to create an image.

```bash
docker build --tag authorcarpentry-docker-articles .
```

We use the tag `authorcarpentry-docker-articles` to be able to identify the image.

No start the image as usual and open the file in RStudio (go to http://localhost:8787 > File > Open File).

```bash
docker run -it -p 8787:8787 authorcarpentry-docker-articles
```

Now you can load and work with the data in R. Analysis example is based on [https://www.r-bloggers.com/building-wordclouds-in-r/](https://www.r-bloggers.com/building-wordclouds-in-r/).

```R
data <- read.csv("articles.csv")
head(data)

library(wordcloud); library(tm)

titles <- VCorpus(VectorSource(data$Title))
titles <- tm_map(titles, PlainTextDocument)
wordcloud(titles)
```

You can learn all about [Dockerfiles in the Docker docs](https://docs.docker.com/engine/reference/builder/).

_How is this useful for reproducible research?_

You can create images tailored to your use case in a transparent way.
If Docker every disappears, at least you will have all the instructions you originally used to create the image.

## Common Dockerfile elements

 **Command** | **Explanation** 
 ----- | -----
`FROM` | specifies which base image, or stack of base images, your image is built on
`MAINTAINER` | specifies who created and maintains the image.
`CMD` | specifies the command to run immediately when a container is started from this image, unless you specify a different command.
`COPY` | will copy new files from a source and add them to the containers filesystem path
`WORKDIR` | sets the current directory for `RUN` and `COPY` statements (preferred over using `RUN cd ..`)
`RUN` | does just that: It runs a command inside the container (eg. `apt-get`)
`EXPOSE` | tells Docker that the container will listen on the specified port when it starts and the host may bind these
`VOLUME` | will create a mount point with the specified name and tell Docker that the volume may be mounted by the host

[based on](https://benmarwick.github.io/UW-eScience-docker-for-reproducible-research/#14)

<!--
Previous: [Saving and Exporting files and projects](03-save-export.html)
-->