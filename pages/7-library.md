---
title: The Experiment Library
pdf: true
permalink: /library
---

# The Experiment Library

The experiment library is available for you to browse at [https://expfactory.github.io/experiments](https://expfactory.github.io/experiments).
It contains over 100 experiments, surveys, and games from the original Experiment Factory, along with community contributions.
From this interface you can browse to an experiment GitHub repository, or preview the experiment right in the browser.

<br>

![{{ site.baseurl }}/assets/img/library.png]({{ site.baseurl }}/assets/img/library.png)

## How does it work?

Each experiment is maintained in a modular fashion in its own GitHub repository. For example, the [big-five-inventory-survey](https://github.com/expfactory-experiments/big-five-inventory-survey) you can find in the linked repository, and the [preview](https://expfactory-experiments.github.io/big-five-inventory-survey/) is on GitHub pages. Since it is part of the [experiment library](https://github.com/expfactory/experiments) that renders to the table above, it is also available [programmatically via API](https://expfactory.github.io/experiments/library.json). This is how it works for the Experiment Factory to [install an experiment](https://expfactory.github.io/generate#library-experiment-selection) (and remember you can install your own local folders, discussed later in that same section). 

## Experiment Containers

The documentation here describing how to build your custom experiment container assumes that you want some custom, special mixture of experiments. However, if you just need a quick survey, we have a collection of [pre-built containers](https://github.com/orgs/expfactory-experiments/packages) ready to go! For example, let's say we want to [run](https://expfactory.github.io/generate#start-your-container) the same big-five-inventory-survey. That would look like this:

```bash
$ docker run -p 80:80 ghcr.io/expfactory-experiments/big-five-inventory-survey start
```
```bash
Database set as filesystem
Starting Web Server

 * Starting nginx nginx
   ...done.
==> /scif/logs/gunicorn-access.log <==

==> /scif/logs/gunicorn.log <==
[2021-11-10 05:04:18 +0000] [1] [INFO] Starting gunicorn 20.1.0
[2021-11-10 05:04:18 +0000] [1] [INFO] Listening at: http://0.0.0.0:5000 (1)
[2021-11-10 05:04:18 +0000] [1] [INFO] Using worker: sync
[2021-11-10 05:04:18 +0000] [33] [INFO] Booting worker with pid: 33
WARNING No user experiments selected, providing all 1
[2021-11-10 05:04:33,246] INFO in utils: [router] big-five-inventory-survey --> big-five-inventory-survey [subid] expfactory/b64c591b-57cf-4eeb-a336-568a5a920d28 [user] dinosaur
[2021-11-10 05:04:36,087] DEBUG in main: Next experiment is big-five-inventory-survey
```

And then open your browser to `127.0.0.1` to see the portal, where you can select and proceed to run the experiment.

![{{ site.baseurl }}/assets/img/portal.png]({{ site.baseurl }}/assets/img/portal.png)

And of course don't forget there are many ways to [customize](https://expfactory.github.io/customize) your container, such as the database so you can collect and analyze your data after, and SSL so you can secure your deployment.

## How do I add an experiment to the library?

You can either develop in your own repository and then submit a pull request to add it to the [library](https://github.com/expfactory/experiments), or feel free to [open an issue](https://github.com/expfactory/experiments/issues) and ping @vsoch to get a repository added to expfactory-experiments. This organization can server not just experiments, but also games and surveys.

<div>
    <a href="/background"><button class="previous-button btn btn-primary"><i class="fa fa-chevron-left"></i> </button></a>
    <a href="/customize"><button class="next-button btn btn-primary"><i class="fa fa-chevron-right"></i> </button></a>
</div><br>
