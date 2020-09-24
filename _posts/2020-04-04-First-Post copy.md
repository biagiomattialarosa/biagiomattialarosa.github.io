---
layout: post
title: "How to organize your research code - Part 1"
description: "A post about my tips on how to organize the research code efficently."
comments: true
---


This post is updated each time I find a better organization. 

I will refer to python code and pytorch because they are the tools that I'm using but it can be adapted to any programming language and framework. 


Objectives are:
- run as fast as possible the experiments
- minimize (or better cancel) lines of code needed to run a different experiment
- minimize (or cancel) the copy-paste code
- ensure fair comparison

Some of these objectives are in contrast each other, therefore this is the best trade-off that I found.

I divide my code in the following dir/files
- architectures: usually a file containing all the architecture that I want compare/use
- datasets: usually a file containing all the code needed to retrieve the data ready to be used in the model. Here are stored ALL the pre-processing steps.
- scripts: usually a folder. Contains all the scripts to run and replicate the experiments. All of them share the same structure, but usually each of them has its own parameters or special constructions.
- novelty: this is the file/dir that usually contain my current research outcome. It can stores my proposed model, layer and so on.

Note the difference between "architectures" and "novelty". The first one contains pre-made architectures that usually you don't modify and are used to compare your approach. The novelty instead contains all the things that you propose. Clearly not always this separation makes sense and sometimes I add my architecture with modified components in the first category. 



The scripts usually have the following ordered structure:
1)  imports
2)  fixed parameters (data dir, device, etc)
3)  seeds
4)  other parameters
5)  datasets
6)  models
7)  optimizations
8)  training
9)  testing
10) printing

### Imports
The first lines of code are import of **all** the libraries that I will use in my code. It is a <a href="https://www.python.org/dev/peps/pep-0008/">standard practice</a> therefore I think we can skip directly to the second point.

### Fixed parameters
This section contain the parameter that are specific for my research but that don't change from an experiment to the other. Examples are:
- data_dir: the dir where it is stored the dataset
- num_runs: the number of runs of each experiment. This is usually a number between 30 and 100.
- log_interval: the number of steps to wait before printing something on the console