---
layout: default
title: Developing an Experiment
pdf: true
permalink: /development
---

# Interactive Development

<quote>This contribution comes from <a href="https://tylerburleigh.com/articles/2018-08/expfactory-task-fork-workflow" target="_blank">one of our users</a>, and has been modified to fit your screen. Thank you @tylerburleigh!</quote>

This page contains recipes for forking an expfactory task and preparing it for an easier development workflow. For example, maybe you want to run a Stroop task, but you want to increase the number of trials, or change the instructions text. You can also take a base task and use that to create something entirely new! Because many cognitive paradigms follow similar procedures, this can really speed up the development time.

## Checklist

To begin, you will need:

* A Linux server with <a href="https://www.docker.com">Docker</a> installed, or your own computer if you run Linux.
* An expfactory task that you want to use as your base, to fork. <br>(Take a look at the <a href="https://expfactory.github.io/experiments/">library of tasks</a>.)
* The ability to SSH into the web server (this is how we access the terminal/console to do stuff; I use PuTTY)

I like to use <a href="https://www.digitalocean.com/">DigitalOcean</a> for my web servers, and for this tutorial I'll be forking the <a href="https://github.com/expfactory-experiments/kirby">kirby task</a>. My linux user is `bitnami`, so you will also be seeing that in the code below.

## Recipes

### Set shell variables

First we'll set some shell variables to make the other recipes more streamlined. `HOME` should point to the home directory for a user on your web server. Since I'm running as the `bitnami` user, I'll put it all there. `TASK` should refer to the task that you want to fork.

```bash
TASK=kirby
HOME=/home/bitnami
```

### Make directories

Like me, for the sake of convenience you'll probably want to access the data and the logs from outside the Docker container. This doesn't impact the containerization. It just lets you access output from the experiment more easily once you have everything up and running.

```bash
mkdir -p $HOME/expfactory/$TASK
mkdir -p $HOME/expfactory/$TASK/data
mkdir -p $HOME/expfactory/$TASK/logs
chmod -R 777 $HOME/expfactory/$TASK/
```

### Generate Dockerfile

Now we'll change to the task directory we created above and build the Dockerfile in that directory.

```bash
# go to directory
cd $HOME/expfactory/$TASK/

docker run -v $HOME/expfactory/$TASK:/data \
  vanessa/expfactory-builder \
  build $TASK
```

> Depending on your Docker installation, you might need to use `sudo` with Docker. It's not recommended to install
in this way, but the note is preserved here since the original post had used it.

Great! Now if you issue a `dir` command you will see the following folders/files: `data  Dockerfile  logs  startscript.sh`

### Build container

Next we'll build the docker container, using the Dockerfile we just created.

```bash
docker build -t expfactory/experiments .
```

### Clone task files to host directory

Now, while we are developing the task, we want to make it as easy as possible to modify "on the fly", even while it is running in a container. To do this, first we must clone the task files from github to a local directory:

```bash
cd /home/bitnami
git clone https://github.com/expfactory-experiments/$TASK.git
chmod -R 777 $TASK
cd $TASK
```

You could imagine here that instead of cloning the repository with the task, you might
have your own local folder you are using instead. We still recommend you put it under version
control, and then perhaps <a href="/contribute.html">contribute it </a> to the library!


### Run container

Now we run the container.
When we run the container, we pass it all of the folders that we created before.

```bash
docker run -d \
   -d -p 80:80 \
   -v $HOME/expfactory/expfactory:/opt/expfactory \
   -v $HOME/expfactory/$TASK/data:/scif/data \
   -v $HOME/expfactory/$TASK/logs:/scif/logs \
   -v $HOME/$TASK:/scif/apps/$TASK \
   expfactory/experiments
```

### Ready to go!

Now it should be up and running. By default, expfactory runs over port 80, so you should be able to access it by typing the URL of your server into a web browser. 

Because of the configuration we've used in these recipes, the task files are served out of `/home/$TASK` on the host-side. This makes it really easy to work with during the development process. The file that you probably want to start hacking away at is `/home/$TASK/experiment.js`, and the data will be stored in `$HOME/expfactory/$TASK/data`. After you've modified the task, you can reload the site in your browser to see the changes live. 

When you finally complete your task, you should make it official by <a href="/contribute.html">contributing it </a> to the library! Happy coding!

<div>
    <a href="/contribute.html"><button class="previous-button btn btn-primary"><i class="fa fa-chevron-left"></i> </button></a>
    <a href="/integrations.html"><button class="next-button btn btn-primary"><i class="fa fa-chevron-right"></i> </button></a>
</div><br>
