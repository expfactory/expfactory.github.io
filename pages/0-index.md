---
title: The Experiment Factory
pdf: true
permalink: /
---

# The Experiment Factory

<div>
    <img src="img/expfactoryticketyellow.png" style="float:left">
</div><br><br>

> Nobody ever comes in... and nobody ever comes out...

<p>And that's the way that reproducible behavioral experiments should be: designed, captured, and used again with assurance of running the same thing.
The Experiment Factory software will help you create a reproducible container to deploy behavioral experiments. Want to jump right in? Choose one of our demo containers, and browse to localhost:</p>


```bash
docker run -p 80:80 vanessa/expfactory-games start
docker run -p 80:80 vanessa/expfactory-surveys start
docker run -p 80:80 vanessa/expfactory-experiments start
```

If you want a more gentle introduction, start with reading some [background]({{ site.baseurl }}/background) on containers and why the Experiment Factory exists in the first place. Then move on to our quick start to [generate](https://expfactory.github.io/generate#quick-start) your own experiment container. Please [give feedback](https://github.com/expfactory/expfactory/issues) about your needs to further develop the software. The [library](https://expfactory.github.io/experiments/) will show you a selection to choose from, including all experiments, surveys, and games migrated from [the legacy Expfactory](https://github.com/expfactory/expfactory-experiments). If you have web-based experiments to contribute, please [reach out](https://github.com/expfactory/expfactory/issues)! Your contributions and feedback are greatly appreciated!

## User Guide

 - [Background]({{ site.baseurl }}/background) for a gentle introduction to containers before the quick start.
 - [Generate]({{ site.baseurl }}/generate) quick starts to generating containers.
 - [Customize]({{ site.baseurl }}/customize) customize container and runtime variables, the database, and other settings.
 - [Usage]({{ site.baseurl }}/usage) of an experiment factory container.
 - [Integrations]({{ site.baseurl }}/integrations) including automated experiment testing robots, generators, and third party tools.

## Developer Guide

 - [Contribute]({{ site.baseurl }}/contribute) an experiment to the [library](https://github.com/expfactory/experiments) for others to use.
 - [Interactive Development]({{ site.baseurl }}/development) suggested practice to develop and debug an experiment interactively in the container

## Library

 - [Browse](https://expfactory.github.io/experiments/) our available experiments [[json]](https://expfactory.github.io/experiments/library.json).
 - [Generate](https://expfactory.github.io/experiments/generate) a custom container from our Library, or
 - [Recipes](https://expfactory.github.io/experiments/recipes) view a pre-generated recipe based on tags in the library.


## Citation

If the Experiment Factory is useful to you, please cite [the paper](https://doi.org/10.21105/joss.00521) to support the software and open source development.

```
Sochat, (2018). The Experiment Factory: Reproducible Experiment Containers. 
Journal of Open Source Software, 3(22), 521, https://doi.org/10.21105/joss.00521
```
[![DOI](http://joss.theoj.org/papers/10.21105/joss.00521/status.svg)](https://doi.org/10.21105/joss.00521)

If you are using the [Legacy software](https://expfactory.github.io/v1/) please cite [this paper](https://www.frontiersin.org/articles/10.3389/fpsyg.2016.00610/full).

```
Sochat VV, Eisenberg IW, Enkavi AZ, Li J, Bissett PG and Poldrack RA (2016) 
The Experiment Factory: Standardizing Behavioral Experiments. 
Front. Psychol. 7:610. doi: 10.3389/fpsyg.2016.00610
```

## Support
You'll notice a little eliipsis (<i class="fa fa-ellipsis-h"></i>) next to each header section. If you click this, you can open an issue relevant to the section, grab a permalink, or suggest a change. You can also talk to us directly on Gitter.

[![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/expfactory/lobby)

We are here for you! You can ask a question directly or open an issue for:

 - [Experiment Factory Core](https://github.com/expfactory/expfactory/issues) 
 - [Experiment Library](https://github.com/expfactory/experiments/issues)
 - [Survey Generator](https://github.com/expfactory/survey-generator/issues)
 - [Expfactory Builder](https://github.com/expfactory/expfactory-builder/issues)
 - [Expfactory Robots](https://github.com/expfactory/expfactory-robots/issues)

If your issue is for a particular experiment, open the issue at the respective repository for the [expfactory-experiments](https://github.com/expfactory-experiments) organization.

<div>
    <a href="/generate"><button class="next-button btn btn-primary"><i class="fa fa-chevron-right"></i> </button></a>
</div><br>
