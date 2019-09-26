---
layout: post
title: "Automating Better Code in Python"
date: 2019-09-26
description: Recently, I've been taking some time to improve my technical skills. I started writing more tests, setting up CI/CD pipelines, and doing automated deployments. Along with the learnings are building tools that I can reuse to optimize my process. As example of it is a docker image that helps me write better code in Python.
---

Recently, I've been taking some time to improve my technical skills. I started writing more tests, setting up CI/CD pipelines, and doing automated deployments. Along with the learnings are building tools that I can reuse to optimize my process. As example of it is a docker image that helps me write better code in Python.

I decided to create a simple [docker image](https://hub.docker.com/r/jpbalbin/python-code-checker) that can format my code properly and adheres to the PEP8 standard as much as possible. While I'm not a fan the character limit per line (I changed mine to 100), I'm trying to follow it to improve how I write code in Python.

To use the docker image, here's the command:
```
docker pull jpbalbin/python-code-checker:0.1
```

The docker image contains two tools: `black` and `pylint`.

Black is so convenient to use. It basically formats your code. There is no need to think more about code formatting. Just run `black` and your code format is basically the same all through out. There is not much configuration can be done. The only config that I changed is the character line limit.

While black formats your code, `pylint` does code analysis in your code. It ensures that you follow the PEP8 standard, error detection, and provide refactoring tips. It also provides a score for your code. I always try to maintain a perfect 10/10 score in pylint.

I used these two tools with these commands:
```
$ docker run --rm -v $(pwd):/app jpbalbin/python-code-checker:0.1 black <.py file / folder>

reformatted fitbit_grapher.py
All done! ✨ 🍰 ✨
1 file reformatted.
```
```
$ docker run --rm -v $(pwd):/app jpbalbin/python-code-checker:0.1 pylint <.py file / folder>

************* Module fitbit_grapher
fitbit_grapher.py:1:0: C0111: Missing module docstring (missing-docstring)
fitbit_grapher.py:7:0: E0401: Unable to import 'matplotlib.pyplot' (import-error)
fitbit_grapher.py:11:0: C0411: standard import "from collections import OrderedDict" should be placed before "import arrow" (wrong-import-order)

-----------------------------------
Your code has been rated at 0.39/10
```

The usual process for me is that I run `black` first to format my code. This ensures that my code will follow PEP8 as much as possible. Afterwards, I run `pylint` to detect PEP8 violations and other ways to improve code.

Another thing about this docker image is that it can easily be integrated into your existing CI/CD pipeline. Black and pylint provide helpful error messages that can stop the integration/deployment. This is good to maintain the readability and code quality of the project.

For black, we can include a `--check` flag to determine what files need to changed without reformatting it.

```
$ docker run --rm -v $(pwd):/app jpbalbin/python-code-checker:0.1 black --check <.py file / folder>
```

Currently, I'm using this docker image for my Python projects. But this still lacks proper code testing. I'm currently reading about testing in Python and how to do it in proper way. I might improve these by adding testing and code coverage tools.