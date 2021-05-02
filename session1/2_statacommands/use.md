---
layout: default
title: Stata Commands - use
nav_order: 1
parent: Stata Commands
grand_parent: Session 1
has_children: false
has_toc: true
---

## ``use``

The ``use`` command loads Stata datasets from the disk, i.e., the datasets present on your computer. A close cousin is the ``sysuse`` command that loads datasets that came pre-installed with Stata (or that are stored on the ado path, whose meaning we don't need to know yet). A more technically advanced cousin is the ``webuse`` command which can load datasets stored on websites. 

You can check what datasets are already available for use with ``sysuse`` by typing ``sysuse dir`` in Stata. One commonly used example is the auto dataset. To use it, type ``sysuse auto``. 

Using the ``use`` command (jeje, you know, how to use ``use``, super bad joke I know) is easy. Type ``use filename, clear`` to load a new dataset that is stored on your computer. filename contains both the address and the name of the dataset. For example, if the covid vaccination data was on your computer's desktop, its address would be similar to "C:/Users/amolr/Desktop/", and so you would type (with adjustments to the address) : 

```
use "C:/Users/amolr/Desktop/covid_vaccination_2021_04_18.dta", clear
```

Up there, ``clear`` is optional. What it tells Stata is to disregard the dataset we are currently working on and to load the new dataset. So, be sure to save the current dataset before loading the new one (if you want to save it, that is). If you already have a dataset loaded in memory to which you have made changes, and don't specify the ``clear`` option with the ``use`` command, Stata will reprimand you by saying "no; data in memory would be lost"!

I used a technical term, "loaded in memory" above. Whenever you load a dataset in Stata, the dataset gets loaded into your RAM for as long as you are working on it in Stata. So, using a dataset is essentially loading it from your hard drive to the RAM. 