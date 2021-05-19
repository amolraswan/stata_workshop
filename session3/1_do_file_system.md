---
layout: default
title: Setting up do files
nav_order: 1
parent: Session 3
has_children: false
---

We previously discussed setting up your [project directory](https://amolraswan.github.io/stata_workshop/session2/1_project_folder/). The need for better organization flows into do-files as well. A medium-sized project will have you clean different datasets, merge them to produce a single or multiple datasets, run regressions, create graphs, etc. Doing all this in a single do-file is chaotic and simply impossible. 

Vinayak Iyer, a PhD student at Columbia, has a short [Stata tutorial](https://github.com/vinayakiyer/MA_StataTutorial) on how to set up your project directory and how to organize the code. We have a few (slight) differences with his approach on the former but I would whole-heartedly endorse his advice on the latter. Navigating projects on Github can be tricky, so check out [this](https://github.com/vinayakiyer/MA_StataTutorial/tree/master/Code) to take a look at his Code folder. You can click on the do-files to view their content. 

First, the do-files are numbered to preserve their order in the folder: 0 for the do-file with globals for file paths, 1 for the cleaning do-files, and 2 for the analysis do-files. Having a single do-file with file path globals also makes it easier to edit them in the future. You can also have a "main" do-file (usually called a "master" do-file) that runs all the other do-files. The command to run a do-file is ``do``.  

We also previously discussed the benefit of a brief description at the start of a do-file. Vinayak's do-files provide a handy template. Besides that, you may want to add the following chunk (which he does so in some of the do-files):

```
clear all 
version ##
set more off
```

1. ``clear all`` drops all objects in the memory but does not affect global or local macros.

2. ``version ##`` allows you to make your code backwards-compatible. For example, if use Stata 15 but specify ``version 13.1``, then Stata will execute the Stata 13.1 version of the commands in your do-file. In most cases, this is inconsequential but in a few instances such as creating random numbers, specifying the version is essential. If you are working in a team, set the version to the lowest common version. If you are working alone, set the version to your current Stata version because it could be that someone uses your code in the future and it would then be helpful for them to know what version commands you had used.

3. When you have a long output, Stata explicitly asks you to click on the more option in the results window to process the next commands. This can be annoying because it pauses code execution. ``set more off`` tells Stata to keep executing the code and not care about output being too long.