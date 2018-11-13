---
title: "Introduction"
teaching: 35
exercises: 0
questions:
- "How can I generalize the structure of my scientific explorations?"
objectives:
- "Introduce the audience to the practical aspects of reproducibility."
keypoints:
- "Scientific exploration pipelines can be recasted as software 
  implementation and maintenance pipelines."
- "Software implementation and maintenance pipelines use sophisticated 
  and mature DevOps tools with large user communities in industry."
- "DevOps tools include (but are not limited to) source code control, 
  package managers, dataset managers, data analysis and visualization 
  tools, and continuous integration services"
- "Popper is a convention that enables and simplifies the use of 
  DevOps tools for scientific exploration pipelines."
---

Many scientific exploration pipelines have the following structure:

![](../assets/img/sci_pipeline.png)

Each of the stages of the above pipeline involve carrying out some (or 
all) of the following tasks:

  * Writing, compiling and packaging code.
  * Configuring computing environments.
  * Executing applications on multiple (local or remote) compute 
    environments.
  * Writing documentation or any type of manuscript (tech reports or 
    scholarly articles).
  * Archiving particular versions of a pipeline so it can be 
    referenced in the future (e.g. by using a DOI generation service).

While one can manually execute these tasks, automating them can not 
only significantly reduce the amount of effort required by others (or 
ourselves) to re-execute a pipeline but, more importantly, allow 
others to have an explicit and easy to understand record of what were 
the series of high-level steps that were executed and in which order. 
The [Popper CLI tool](https://github.com/systemslab/popper) aids 
practitioners (students and researchers) in implementing and 
automating pipelines by writing shell scripts for each stage. In this 
lesson, you will learn how to generate pipelines that are easier to 
re-execute, validate and maintain.

### The DevOps Toolkit

As we will experience first-hand throughout this lesson, the more 
complex a pipeline gets, the more the time we need to invest on issues 
that are out of the scope of our domain. Things such as dealing with 
multiple changes to code, managing distinct environment 
configurations, handling parametrized executions (just to name a few) 
increase significantly the cognitive load associated to the 
implementation and maintenance of a pipeline.

Fortunately, the list of tasks shown above (writing code, configuring 
an environment, etc.) are  not unique to the scientific computing 
world and in fact are carried out by software engineers on a 
day-to-day basis. The following table shows a one-to-one task 
correspondence between the two domains:

| Scientific Exploration       | Software Project          |
| ---------------------------- | ------------------------- |
| Experiment code              | Source code               |
| Input / output data          | Test data                 |
| Analysis and Visualization   | Test analysis             |
| Validation                   | Regression testing        |
| Manuscript / notebook        | Documentation / reports   |

Whereas a pipeline for a scientific exploration has the goal of 
generating reproducible research, pipelines found in open source 
software ([OSS](https://en.wikipedia.org/wiki/Open-source_software) 
and [DevOps](https://en.wikipedia.org/wiki/DevOps)) projects target 
"Software Reproducibility", i.e. systematically reproduce bugs in 
order to have control over the quality of a software project.

Not surprisingly, OSS/DevOps communities have created tools and 
services whose goal is to ease the implementation and maintenance of 
pipelines. This set of tools is sometimes referred to as the [DevOps 
toolbox](https://xebialabs.com/periodic-table-of-devops-tools/). The 
following is a small sample of some mainstream tools, by category:

  * Source control. [Git](http://git-scm.com), 
    [Svn](https://subversion.apache.org) and 
    [Mercurial](https://www.mercurial-scm.org) are popular VCS tools. 
    [GitHub](http://github.com), [GitLab](http://gitlab.com) and 
    [BitBucket](https://bitbucket.org) are web-based Git repository 
    hosting services. They offer all of the distributed revision 
    control and VCS functionality of Git as well as adding their own 
    features. The entire history of the project and its artifacts of 
    public repositories can be browsed online.

  * Package managers. [Docker](http://docker.com) automates the 
    deployment of applications inside software containers by providing 
    an additional layer of abstraction and automation of 
    operating-system-level virtualization on Linux. Alternatives to 
    Docker are modern package managers such as 
    [Nix](https://nixos.org/nix/) or 
    [Spack](https://github.com/LLNL/spack), or, in the case of virtual 
    machines, [Vagrant](http://vagrantup.com).

  * Dataset Management. While it is possible to store data in a code 
    repository, traditional VCS tools such as Git were not designed to 
    store large binary files. A proper artifact repository or dataset 
    management tool can take care of handling data dependencies. 
    Examples are [Apache Archiva](https://archiva.apache.org), 
    [Git-LFS](https://www.nmc-probe.org), 
    [Datapackages](http://frictionlessdata.io/data-packages/), 
    [Artifactory](https://www.jfrog.com/artifactory), 
    [ckan.org](https://ckan.org) and [data.world](https://data.world). 

  * Data Analysis and Visualization. [Jupyter](http://jupyter.org) 
    notebooks run as a web-based application. It facilitates the 
    sharing of documents containing live code (in Julia, Python or R). 
    [Binder](http://mybinder.org) is service that allows one to turn a 
    GitHub repository into a collection of interactive Jupyter 
    notebooks so that readers do not need to deploy web servers 
    themselves. Alternatives to Jupyter are 
    [Gnuplot](http://gnuplot.sourceforge.net), 
    [Zeppelin](http://zeppelin.apache.org) and 
    [Beaker](http://beakernotebook.com). Other scientific 
    visualization such as [Paraview](http://paraview.org) and 
    [Gephi](https://gephi.org) tools can also fit in this category.

  * Continuous Integration. [Travis CI](https://travis-ci.org/) is an 
    open-source, hosted, distributed continuous integration service 
    used to build and test software projects hosted at GitHub. 
    Alternatives to Travis CI are [CircleCI](https://circleci.com) and 
    [CodeShip](https://codeship.com). Other self-hosted solutions 
    exist such as [Jenkins](http://jenkins-ci.org).

### The Popper Convention

A list of high-level guidelines that make it easier to manage and 
maintain a pipeline over time is the following:

 1. For each stage of the scientific exploration pipeline being 
    implemented, pick one or more tool from the DevOps toolkit (see 
    below for what we refer with this).
 2. Write portable scripts for each stage of the pipeline, and put all 
    of them in version control, in order to provide a self-contained 
    repository.
 3. As a pipeline evolves over time, document changes in the form of 
    version control commits.

We refer to this as the Popper Convention (more on [the paper on 
Popper](https://github.com/systemslab/popper-paper/raw/master/paper/paper.pdf)). 
In this lesson, we will make us of Bash, Git, TravisCI and Docker. 
Following the convention and using the CLI tool will allow us to 
generate pipelines that are easy to re-execute, validate and maintain 
over time.
