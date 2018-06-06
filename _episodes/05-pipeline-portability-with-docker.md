---
title: "Creating Portable Pipelines"
teaching: 0
exercises: 0
questions:
- 'How can I easily run a pipeline on other machines?'
objectives:
- "Show how to generate portable pipelines using virtualization 
  technologies."
keypoints:
- "First key point."
---

In the previous two sections we worked with a pipeline that has few 
dependencies on the environment: a minimal installation of Python is 
all that is needed. This level of simplicity is rarely found in real 
world experimentation pipelines. Instead, it is common to make use of 
3rd party libraries or domain-specific software stacks that allow 
researchers to save time when carrying out scientific explorations. 
One of the implications of this is that, the more complex a pipeline 
gets, the more time we need to invest on **properly** setting up the 
computational environment needed to successfully execute a pipeline 
and reproduce the associated results.

To illustrate some of the portability issues that we can encounter, we 
will attempt to execute a pipeline that has been implemented by 
someone else. The `popper` command has search and import capabilities 
that allow users to browse through a list of popperized repositories 
and find particular pipelines. To get a list of available pipelines:

```bash
popper search popper
```

the `search` command takes any keyword and tries to match it to the 
names of available pipelines (by default, it looks in the 
[`popperized`](https://github.com/popperized) github organization). We 
will be working with a data science pipeline, so lets add it to our 
repository:

```bash
popper add popperized/swc-lesson-pipelines/data-science-no-stages
```

Once the above executes, we can show that it has been added to our 
repository:

```bash
ls -l pipelines/data-science-no-stages
```

The pipeline consists of a `scripts/` folder and, as the name implies 
(and for illustration purposes), it has no stages, so let's implement 
`run`, `generate-figures` and `validate` stages. For the first, we 
create the file `pipelines/data-science-no-stages/run.sh` with the 
following content:

```bash
#!/bin/bash
python scripts/generate-learning-curves.py
```

we then create the 
`pipelines/data-science-no-stages/generate-figures.sh` file with the 
following content:

```bash
#!/bin/bash
python scripts/generate-figures.py
```

and the `validate.sh` script:

```bash
#!/bin/bash
python scripts/compare-output.py
```

lastly, we update the popper pipeline so that it now includes these 
two stages:

```bash
popper stages --set=run,generate-figures data-science-no-stages
```

We now try to run it:

```bash
popper run data-science-no-stages
```

As you might be expecting by now, the execution of this pipeline 
likely fails on the machine where it is being executed. The main 
reason is that these scripts assume that `numpy`, `pandas`, `sklearn` 
and `matplotlib` are available in the environment where the pipeline 
runs, which is not necessarily the case.

Even if these packages are available on your local machine, it is 
likely that the version of these packages being used might not 
correspond to what was used when this pipeline was originally 
implemented. As an exercise, if you happened to have these packages 
installed on your machine, can you look at the output of the 
`validate.sh` stage? Did it result in having the same figures?

### Portable Pipelines With Docker

This ["dependency 
hell"](https://en.wikipedia.org/wiki/Dependency_hell) situation is as 
old as computers and, not surprisingly, over the years software 
engineering communities have developed technologies to minimize the 
problems associated to this type of scenario. One of these 
technologies is 
[virtualization](https://en.wikipedia.org/wiki/Virtualization), by 
which isolated computational environments can be created (and moved 
across machines) in order to have complete control of what software 
gets installed.

An alternative tool for creating isolated environments is 
[Docker](https://en.wikipedia.org/wiki/Docker_(software)), the popular 
software container solution that is widely used in Cloud Computing 
environments. Another version of the same pipeline that makes use of 
containers is available. In order to import it into your repository, 
you can execute:

```bash
popper add popperized/swc-lesson-pipelines/docker-data-science
```

Once you download this, you can look at the available stages:

```bash
popper stages docker-data-science
```

You can see that there is a `setup` phase that builds a Docker 
container image by using the contents of the `docker/` folder. To 
learn more about how images are build, see 
[here](https://docs.docker.com/engine/reference/commandline/build). To 
finalize, let's run it on our machine:

```bash
popper run docker-data-science
```


And as you can see, the above succeeds (as long as you have a working 
version of Docker). For completeness, let's remove the first (not 
portable) pipeline:

```
popper rm data-science-no-stages
```

And commit the one that actually ran without problems:

```bash
git add .
git commit -m 'Adds a dockerized data science pipeline'
```

### Additional Virtualization Tools

In addition to Docker, other tools that can help to create portable 
pipelines exist, depending on your requirements:

  * [`virtualenv`](https://virtualenv.pypa.io/). If a pipeline is only 
    using python, then `virtualenv` might be easier/faster to use than 
    Docker. An example of such a pipeline can be found 
    [here](https://github.com/popperized/swc-lesson-pipelines/tree/master/pipelines/sea-surface-mapping) 
    (add it to your repo by doing `popper add 
    popperized/swc-lesson-pipelines/sea-surface-mapping`)

  * [`vagrant`](https://www.vagrantup.com/). Vagrant is an automation 
    tool that runs on top of hardware virtualization technologies such 
    as [VirtualBox](https://www.virtualbox.org/) or 
    [VMWare](https://www.vmware.com/products/fusion.html). An example 
    of how to use it in a pipeline is 
    [here](https://github.com/popperized/popper-readthedocs-examples/tree/master/pipelines/linux-cgroups).

  * `R`'s [`packrat`](https://rstudio.github.io/packrat/). Example 
    pipeline coming soon.

  * [`spack`](https://github.com/spack/spack). A [functional package 
    manager](https://en.wikipedia.org/wiki/Nix_package_manager) that 
    makes it possible to "install a new version of a package without 
    breaking existing installations, so many configurations of the 
    same package can coexist". An example pipeline can be found 
    [here](https://github.com/popperized/popper-readthedocs-examples/tree/master/pipelines/mpip).
