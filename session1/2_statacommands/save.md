---
layout: default
title: save
nav_order: 9
parent: Stata Commands
grand_parent: Session 1
has_children: false
---

It's now time to save the dataset you've been working on. Before learning how to save your dataset, however, remember the golden rule:

> Never over-write your original dataset

Now that this is out of the way, it is very simple to save:

```
save "C:/Users/amolr/Desktop/covid_vaccination_2021_04_18_edited.dta", replace
```

``replace`` tells Stata to overwrite if the file already exists (which is why you have to be super careful with ensuring that the filename is not of your original dataset). Once you start working with do files, you will make changes to the do file over time but will not keep creating newer datasets everytime you run it. Instead, you can simply update the end product (i.e., the edited dataset) by including the ``replace`` option. Again, never over-write your original dataset!