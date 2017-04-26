Author Carpentry : Docker for reproducible research
=======

<div style="color: #ff1111;">
<strong>This course uses the Author Carpentry template but is not an Author Carpentry lesson yet!</strong> Find out more on the progress of this project at <strong><a href="https://github.com/AuthorCarpentry/planning/issues/3">https://github.com/AuthorCarpentry/planning/issues/3</a></strong>.</div>

Reproducibility of computational results is crucial in modern algorithm-based research.
In this lesson, we introduce Docker as a useful tool to (a) document your computational environment, and (b) make a computational environment transferable across machines and thus archivable.
The intention of this course is to showcase Docker as a useful tool for scientists, even if they are _not_ regular users of the command line, which this course is completely based on.

*Content Contributors: Daniel N&uuml;st*

*Lesson Maintainers: Daniel N&uuml;st*

**Lesson status: In Development**

## Learning Objectives:

- Docker basics (images, Dockerfiles, containers)
- RStudio in a container
- Jupyter Notebook in a container
- Archival of software and runtime environments with Docker
- Creating reproducible runtime environments from manifests

## Topics:

1. [Getting started with Docker](00-getting-started.html)
2. [RStudio in a Docker container](01-rstudio-in-container.html)
3. [Jupyter in a Docker container](02-jupyter-in-container.html)
4. [Transfer and archive of containers](03-transfer-and-archive.html)
4. [Create an image from a Dockerfile](06-dockerfile.html)

### Optional

- [Templates for reproducible research](05-templates.html)
- [More geospatial tools in containers](04-geocontainers.html)

<!--
## Data

Data files for the lesson are available here: 
-->

## Scope of this lesson

This lesson provides a rather _"raw and manual"_ approach to creating reproducible packages of data, code, and the required runtime environment.
Making this potentially tedious process more comfortable and ideally automatic for users is an active field of research, see for example the [Executable Research Compendium](http://dx.doi.org/10.1045/january2017-nuest) by the [o2r project](http://o2r.info), and tools such as [ReproZip](http://reprozip.org/).
Naturally understanding in depth how reproducibility can be achieved provides a clear advantage over simply using a white box (the existing tools are all open, so there is no black box).
Therefore this lesson's contents on concepts or containerization/virtualization and the leading open source tool are surely worth knowing, even when using supporting tools and services.
This also makes this topic suitable for a generic audience interested in Author Carpentry.

## Requirements

Author Carpentry's teaching is hands-on, so participants are encouraged to use their own computers to insure the proper setup of tools for an efficient workflow.
*These lessons assume no prior knowledge of the skills or tools*, but working through this lesson requires working copies of the software described below.
To most effectively use these materials, please make sure to install everything *before* working through this lesson.                    

- [Docker](https://www.docker.com/get-docker)
- editor with highlighting, e.g. [vscode](https://code.visualstudio.com/)
<!-- - [Docker ID](https://hub.docker.com/register/) for an account on [Docker Hub](https://hub.docker.com/) -->
<!-- - [GitHub account](https://github.com/join) -->
