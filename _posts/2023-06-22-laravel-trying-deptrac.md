---
layout: post
title:  Laravel trying deptrac
date:   2023-06-22 22:25:00
description: Deptrac, a great php tool
tags: laravel php deptract
categories: code
---
A few days ago, I was testing a tool for analyzing the structure of a project and enforcing certain rules, mainly related to dependencies.

The library in question is called deptrac, and its documentation can be found in the following link: https://qossmic.github.io/deptrac/

This tool allows developers to specify the project's structure in the form of layers using a YAML file. It then allows them to indicate the dependencies that exist (that are going to be rules the project should enforce) between the different layers.

After installing it, I tried running it on an existing project at the company where I am currently working. For this purpose, I created a deptrac.yaml file in the root of the Laravel project, that contains the following structure and rules:

```yaml
deptrac:
  paths:
    - ./app
  layers:
    - name: Controller
      collectors:
        - type: className
          value: .*Controller.*
    - name: Repository
      collectors:
        - type: className
          value: .*Repository.*
    - name: Service
      collectors:
        - type: className
          value: .*Service.*
    - name: Model
      collectors:
        - type: directory
          value: .*Models*
  ruleset:
    Controller:
      - Service
    Service:
      - Repository
    Repository:
      - Model
    Model: ~
```


Next, I used the following command to generate a report that provides information about rule violations:

```bash
php vendor/bin/deptrac analyse
```

This command analyzes the project's structure based on the rules defined in the deptrac.yaml file and generates a report highlighting any violations found.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2023-06-22-laravel-trying-deptrac/deptrac-report.JPG" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Finally, I used the tool to generate an image that visualizes the dependencies between different layers, with red lines indicating violations of the rules defined in the YAML file.

The specific command used to generate this image depends on the configuration and options of the deptrac tool. However, a common command to generate the image could be:

```bash
php vendor/bin/deptrac --formatter=graphviz-display
```

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2023-06-22-laravel-trying-deptrac/deptrac-image.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>