---
title: Customize your Experiment Container
pdf: true
permalink: /customize
---

# Custom Configuration

> Note that these pages describe variables to customize the experiment container. See [participant variables]({{ site.baseurl }}/usage#participant-variables) for customizing experiments.

You have probably just reviewed the basics of [generation of a container](/generate) and now are ready to customize it. For example, if you want more specificity to configure your container, you might want to customize the database or experiment variables. There are **two** kinds of customization, the customization that happens **before** you build the container (for example, the experiments you choose to install, period, and any defaults you want set for running them) and the customization that happens at runtime (meaning defining the database type when you start the container).

If you change the defaults, this means that any users that run your container (without specifying these variables) will get these as default. If you want your container to be most usable by others, we recommend that you don't do this, and keep the defaults as the most flexible types - a flat file system database and general study id (expfactory).

If you leave these defaults, you (and the future users of your container) can then easily customize these variables when the container is started in the future. The risk of setting a default database like `sql` or `postgres` is that a user that doesn't know some credential needs to be defined won't be able to use the container. 

The choice is up to you! For settings defaults at build time, see the next section [default variables](#default-variables). For setting at runtime, see the next page for [starting your container](/usage.html#start-the-container).
 
## Default Variables
When you run a build with `quay.io/vanessa/expfactory-builder` image, there are other command line options available pertaining to the database and study id. Try running `docker run quay.io/vanessa/expfactory-builder build --help` to see usage. If you customize these variables, the container recipe generated will follow suit.

### database
We recommend that you generate your container using the default "filesystem" database, and customize the database at runtime. A **filesystem** database is flat files, meaning that results are written to a mapped folder on the local machine, and each participant has their own results folder. This option is provided as many labs are accustomed to providing a battery locally, and want to save output directly to the filesystem without having any expertise with setting up a database. This argument doesn't need to be specified, and would coincide with:

```bash
docker run -v /tmp/my-experiment:/data \
              quay.io/vanessa/expfactory-builder \
              build --database filesystem \
                      tower-of-london
```

Your other options are **sqlite**, **mysql**, and **postgres** all of which we recommend you specify when you start the image.

### randomize
By default, experiments will be selected in random order, and it's recommended to keep this. The other option will use the ordering of experiments as you've selected them. If you want a manually set order, then after you use the `expfactory-builder`, edit your Dockerfile by adding the following environment variable:

```dockerfile
ENV EXPFACTORY_RANDOM true
```

This variable can be easily changed at runtime via a checkbox, so it's not hugely important to set here.


### studyid

The Experiment Factory will generate a new unique ID for each participant with some study idenitifier prefix. The default is `expfactory`, meaning that my participants will be given identifiers `expfactory/0` through `expfactory/n`, and for a filesystem database, it will produce output files according to that schema:

```bash
 /scif/data/
      expfactory/
           00000/
            tower-of-london-result.json
```

To ask for a different study id:

```bash
docker run -v /tmp/my-experiment:/data \
              quay.io/vanessa/expfactory-builder \
              build --studyid dns \
                      tower-of-london
```

Again, we recommend that you leave this as general (or the default) and specify the study identifier at runtime. If you want to preserve a container to be integrated into an analysis exactly as is, then you would want to specify it at build.


### output

You actually **don't** want to edit the recipe output file, since this happens inside the container
(and you map a folder of your choice to it.) Note that it is a variable, however, if you need to use expfactory natively and want to specify a different location.


## Environment Variables
Many of the custom variables, along with runtime variables that you want to set as defaults, can be specified in the environment. This typically means building your experiment container with the variable defined (e.g., in the Dockerfile, usually like `ENV EXPFACTORY_STUDY_ID expfactory`). Here we will provide a tabular overview of these variables. The first set are pertinent to runtime variables. Setting runtime variables in the environment will make them defaults for your container, but they can be overriden by the user at runtime.

## Runtime Variable Table 

| Variable | Default | Command Line Option | Definition |
|-----------|----------|------------|------------------|
| EXPFACTORY_STUDY_ID | expfactory | `--studyid` |the study identifier is used (for a flat filesystem database) as the base folder name |
| EXFACTORY_RANDOM | true | `--randomize` or `--no-randomize` | present the experiments in random order |
| EXPFACTORY_DATABASE | filesystem | `--database`| the database to use by default (can be overriden by user at runtime) |
| EXPFACTORY_HEADLESS | false | `--headless`| hide the experiment selection portal and require token ids for entry |
| EXPFACTORY_EXPERIMENTS | undefined | `--experiments` | A list of experiments to subset the portal to on a session start. Default is undefined, meaning all experiments in the container are deployed. |
| EXPFACTORY_RUNTIME_VARS | undefined | `--vars`| a file with variables to pass to experiments with POST | 
| EXPFACTORY_RUNTIME_DELIM | `\t` (TAB) | `--delim`| the delimiter to separate columns in the variables file | 

### Install Variables

The next set are relevant for installation.

| Variable | Default | Command Line Option | Definition |
|-----------|----------|------------|------------------|
| EXPFACTORY_REGISTRY_BASE | expfactory.github.io | NA | the registry base to install from |
| EXPFACTORY_LIBRARY | `EXPFACTORY_REGISTR_BASE/experiments/library.json` | NA | the library json to install from |
| EXPFACTORY_BRANCH | master | NA | when building, the branch from expfactory to install from. Useful for development |
| EXPFACTORY_DATA | /scif/data | NA | the base for data, defaults to [Scientific Filesystem](https://sci-f.github.io) $SCIF_DATA |
| EXPFACTORY_BASE | /scif/apps | NA |the base for experiments, defaults to [Scientific Filesystem](https://sci-f.github.io) $SCIF_APPS 
| EXPFACTORY_LOGS | /scif/logs | NA | folder to store `expfactory.log` in |
| EXPFACTORY_COLORIZE | true | NA | print colored debugging to the screen |
| EXPFACTORY_SERVER | localhost | NA | the server address, usually localhost is appropriate |

Note that bases for expfactory were initially provided on [Docker Hub](https://hub.docker.com/r/vanessa/expfactory-builder/tags) and have moved to [Quay.io](https://quay.io/repository/vanessa/expfactory-builder?tab=tags). Dockerfiles in the repository that use the expfactory-builder are also updated. If you need a previous version, please see the tags on the original Docker Hub.

## Expfactory wants Your Feedback!
The customization process is very important, because it will mean allowing you to select variable stimuli, lengths, or anything to make a likely general experiment specific to your use case. To help with this, please [let us know](https://github.com/expfactory/expfactory/issues) your thoughts.

<div>
    <a href="/generate"><button class="previous-button btn btn-primary"><i class="fa fa-chevron-left"></i> </button></a>
    <a href="/usage"><button class="next-button btn btn-primary"><i class="fa fa-chevron-right"></i> </button></a>
</div><br>
