---
layout: post
title: "Installing Graph-tool in Virtualenv or Pyenv"
date: 2018-12-07
---

We are using [graph-tool](https://graph-tool.skewed.de/) by [Tiago Peixoto](https://skewed.de/tiago) at [Indigo Research](https://www.indigoresearch.xyz/). It is a handy open source tool for doing graph analysis and manipulation in Python. Unfortunately, we had a hard time installing it to some of our dev machines using Ubuntu 16.04 and Python 3.6+.

**Problem:**

Graph-tool doesn't appear to be installed even after doing the installation instructions from the [graph-tool docs](https://git.skewed.de/count0/graph-tool/wikis/installation-instructions#debian-ubuntu).

The installation using `xenial` distribution for Ubuntu works smoothly. Although, importing `graph_tool` will still output `ModuleNotFoundError`.

```
Python 3.7.0 (default, Sep  6 2018, 07:30:03)
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from graph_tool.all import *
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'graph_tool'
```

The problem was because the default Python version of Ubuntu 16.04 is still at `Python 3.5.2`. Thus, graph-tool was installed in the default Python. In my case, it is in `/usr/lib/python3/dist-packages`.

That's why different version of Python in virtualenv or installed using pyenv can't find graph-tool.

**Solution:**

We need to direct the venv or pyenv to where graph-tool exists in our system. To do this, we need to go to the `site-packages` folder of the specific python version we're using in the venv.

```
$ cd /path/to/env/<version_name>/lib/python3.7/site-packages
$ touch dist-packages.pth
$ echo "/usr/lib/<default_version>/dist-packages" >> dist-packages.pth
```

In my case, replacing those versions, here are the commands that I used.

```
$ cd ~/.pyenv/versions/3.7.0/lib/python3.7/site-packages
$ touch dist-packages.pth
$ echo "/usr/lib/python3/dist-packages" >> dist-packages.pth
```

Those commands created a `dist-packages.pth` file in the `site-packages` folder of the specific Python version we're using. This instructs the the venv to also check the packages in that folder when we try to import a package.

To verify that graph-tool is now working as intended, run this command with your venv activated:

```
$ (env) python3 -c "from graph_tool.all import *"
```

If there are no errors, graph-tool is now successfuly installed.

Credits to this solution I found written in a [Github Gist](https://gist.github.com/goweiting/b3a8c67c0f7ad376d3ce73f2c7729224).