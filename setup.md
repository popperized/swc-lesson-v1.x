---
layout: page
title: Setup
root: .
---

You need to have the following software installed on your computer to
follow this lesson.

# Bash

Bash is a commonly-used shell that gives you the power to do simple 
tasks more quickly.

### Windows

If you are on Windows 10, we highly recommend to install the [Windows 
Subsystem for 
Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10), 
which will give you a full Linux environment. On older versions of 
Windows, we recommend you download and install a linux `xterm` 
emulator such as [MobaXterm](https://mobaxterm.mobatek.net/) or 
[Cygwin](http://cygwin.com/) to use with Git and Docker. The commands 
in this lesson assume a [POSIX-compliant 
Unix](https://en.wikipedia.org/wiki/POSIX), so having an emulator will 
allow for a better learning experience.

### macOS

The default shell in all versions of macOS is Bash, so no need to 
install anything. You access Bash from the Terminal (found in 
`/Applications/Utilities`). See the [Git installation 
video](https://www.youtube.com/watch?v=9LQhwETCdwY) tutorial for an 
example on how to open the Terminal. You may want to keep Terminal in 
your dock for this workshop.

### Linux

The default shell is usually Bash, but if your machine is set up 
differently you can run it by opening a terminal and typing `bash`. 
There is no need to install anything.

# Git

[Git](https://git-scm.com/) is a version control system that lets you 
track who made changes to what (and when) and has options for easily 
updating a shared or public version of your code on 
[GitHub](https://github.com), [BitBucket](https://bitbucket.org/) or 
[GitLab](https://gitlab.com).

For this lesson, you will need an account at GitHub for parts of this 
lesson. Basic GitHub accounts are free. We encourage you to create a 
GitHub account if you don't have one already. You will need a 
supported web browser in order to use the web interface of these 
services (current versions of Chrome, Firefox or Safari, or Internet 
Explorer version 9 or above).

For students, GitHub offers the [Student Developer 
Pack](https://education.github.com/pack) which offers free access to 
some developer tools and services that you would otherwise need to pay 
for.

### macOS

For OS X 10.9 and higher, install Git for Mac by downloading and 
running the most recent installer from [this 
list](https://sourceforge.net/projects/git-osx-installer/files/). 
After installing Git, there will not be anything in your 
`/Applications` folder, as Git is a command line program.

Alternatively, you can use [`homebrew`]() to install Git and many 
other packages.

### Linux

If Git is not already available on your machine you can try to install 
it via your distro's package manager. For Debian/Ubuntu run `sudo 
apt-get install git` and for Fedora run `sudo dnf install git`.

### Windows

Git packages are available for unix terminal emulators such as cygwin. 
If you installed the Linux subsystem, then you can use the package 
manager of the corresponding distribution to install it.

# Popper

To get started with the CLI tool, please install Popper by following 
the instructions on [this 
page](https://github.com/systemslab/popper/tree/master/cli#install). 
Note that we have only thoroughly tested on macOS and Linux. For 
Windows, we recommend using Popper with the [Windows Subsystem for 
Linux](https://msdn.microsoft.com/en-us/commandline/wsl/install-win10). 

To get an overview and list of commands check out the command line 
help:

```bash
popper --help
```

# Docker

In order to run the more advanced examples of this lesson, Docker will 
need to be available on your machine. Please visit 
<https://www.docker.com> to download and install the version 
compatible with your system.

Make sure you can run the `hello-world` example provided by Docker to 
confirm your installation was successful. More information about 
getting started and running hello-world can be found at 
https://docs.docker.com/get-started/.

> **NOTE**: Due to time constraints, we can't provide Docker 
> installation support. We suggest contacting your system 
> administrator or consulting the Docker documentation and forums if 
> problems are encountered.

# Python

Python is a popular language for research computing, and great for 
general-purpose programming as well. For this lesson, a minimal 
installation of **Python 2.7** is required, which is available by 
default on macOS and Linux, as well as on unix terminal emulators for 
Windows such as Cygwin.

# Text Editor

When you're writing code, it's nice to have a text editor that is 
optimized for writing code, with features like automatic color-coding 
of key words. The default text editor on macOS and Linux is usually 
set to Vim, which is not famous for being intuitive. If you 
accidentally find yourself stuck in it, try typing the escape key, 
followed by `:q!` (colon, lower-case 'q', exclamation mark), then 
hitting Return to return to the shell.

An easier to use editor available on all platforms is 
[`nano`](https://en.wikipedia.org/wiki/GNU_nano). It is available by 
default on macOS and Linux. See the [Git installation]() video 
tutorial for an example on how to open nano. It should be 
pre-installed.
