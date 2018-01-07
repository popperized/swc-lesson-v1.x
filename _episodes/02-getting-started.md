---
title: "Popper Pipelines"
teaching: 0
exercises: 0
questions:
- "How can I automate a scientific exploration pipeline?"
objectives:
- "Introduce reader to the concept of Popper pipelines."
keypoints:
- 'The `popper` command line interface allows convenient creation of 
  “popperized” pipelines with scaffolding that can be tested from the 
  beginning.'
- 'Popper pipelines can be shared via github (or similar services)'
---

We first need to install the CLI tool by following [these 
instructions](https://github.com/systemslab/popper/tree/master/popper#install). 
Show the available commands:

```bash
popper help
```

Show which version you installed:

```bash
popper version
```

> **NOTE**: this exercise was written using 0.5

Create a project repository (if you are not familiar with git, look 
[here](https://www.learnenough.com/git-tutorial)):

```bash
mkdir mypaper
cd mypaper
git init
echo '# mypaper' > README.md
git add .
git commit -m 'first commit'
```

Initialize the popper repository and add the configuration file to git:

```bash
popper init
git add .
git commit -m 'adds .popper.yml file'
```

### New pipeline

Initialize pipeline using `init` (scaffolding):

```bash
popper init myexp
```

Show what this did:

```bash
ls -l pipelines/myexp
```

Commit the "empty" pipeline:

```bash
git add pipelines/myexp
git commit -m 'adding myexp scaffold'
```

### Executing a pipeline

Run popper check:

```bash
cd pipelines/myexp
popper check
```

> **NOTE:** By default, `popper check` runs all commands directly on 
the host. We recommend running an isolated environment. In order to do 
this, one can create a pipeline using the `--env` flag of the `popper 
init` command. For example, `popper init <pipeline> --env=alpine-3.4` 
runs a command inside an `alpine-3.4` container.

Once a pipeline is checked, one can show the logs:

```bash
ls -l popper_logs
```

### Adding Project to GitHub

Create a repository on github and upload our commits:

```bash
# set the new remote
git remote add origin <your-github-repo-url>

# verify the remote URL
git remote -v

# push changes in your local repository up to github
git push -u origin master
```
