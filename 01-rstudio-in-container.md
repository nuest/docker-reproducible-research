#  RStudio in a Docker container

5 minutes 

---------------------------------------------------

## Learning Objectives

* start RStudio in a container
* learn about Rocker image variants

----------------------------------------------------

## Starting RStudio

[RStudio](http://rstudio.com/) is a popular IDE for the [R](http://r-project.org/) language and environment for statistical computing and graphics.

[Ben Marwick](https://github.com/benmarwick) demonstrates in his [_research compendium_](https://github.com/benmarwick/1989-excavation-report-Madjebebe) how to use a containerised version of RStudio and why.
In brief, he _only_ used the container to develop an R package, which contains all of the computations for a scientific article he co-authored.

> _I developed and tested the package on this Docker container, so this is the only platform that I'm confident it works on, and so recommend to anyone wanting to use this package to generate the vignette, etc._

By only working within the container, he created a transferable execution environment.
His host operating system is free for experimentation and to be secure (e.g. installing a later library version) without risking the integrity of the combination of packages in the container.

The _performance overhead_ for running RStudion in a container is negligent for most use cases, unlike you might know from virtual machines (cf. [slides by B. Marwick](https://benmarwick.github.io/UW-eScience-docker-for-reproducible-research/#3)).

Here is all you need to start it:

```bash
$ docker run -p 8787:8787 rocker/rstudio
# stop the container with Ctrl+c
```

Using the CLI option `-p` we expose a [port](https://en.wikipedia.org/wiki/Port_(computer_networking)) of the container to our host computer.

No open the UI in your browser: **http://localhost:8787** and sign-in with rstudio/rstudio.
You can install packages and run analyses now just as in your regular RStudio version, of course ideally by using [executable documents with Markdown](https://authorcarpentry.github.io/executable-documents-rstudio/).

## Rocker images

We use an image from the [Rocker](https://github.com/rocker-org/rocker) organisation (see the [Rocker announcement for some background](http://dirk.eddelbuettel.com/blog/2014/10/23/)).
Rocker published different variants of images for R targeted at different use cases.

They provide **base images**](https://github.com/rocker-org/rocker#base-docker-containers) and also images with different collections of pre-installed packages, the [**use case**](https://github.com/rocker-org/rocker#use-cases) images.

If you are a useR, these should get you started quickly.

_How is this useful for reproducible research?_

You can easily try out and compare different R versions using the [`r-ver`](https://hub.docker.com/r/rocker/r-ver/tags/) images.

```bash
$ docker run -it rocker/r-ver:3.1.0
# [image download log]

R version 3.1.0 (2014-04-10) -- "Spring Dance"
Copyright (C) 2014 The R Foundation for Statistical Computing
Platform: x86_64-unknown-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

> 1+1
[1] 2
> q()
```

This gives you an interactive session of R in a specific version. Nice!
You can leave the R session just as a regular R session by typing `quit()`.

## More resources on Docker and R

- [_Investigating Docker and R_](http://o2r.info/2016/12/15/investigating-docker-and-R/) by the o2r project team (blog post)
- [_Reproducible Research using Docker and R_](https://benmarwick.github.io/UW-eScience-docker-for-reproducible-research/#1) by B.Marwick (presentation slides)
- [_An introduction to Docker for reproducible research_](https://doi.org/10.1145/2723872.2723882) by Carl Boettiger (research article)


<!--
Previous: [Getting Started with OpenRefine](00-getting-started.html)  Next: [Scripts from OpenRefine](02-scripts.html)
-->