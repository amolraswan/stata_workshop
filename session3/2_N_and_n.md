---
layout: default
title: \_N and \_n (and indexing)
nav_order: 2
parent: Session 3
has_children: false
---

``_N`` equals the number of observations in the dataset. To see, try ``display _N``. On the other hand, ``_n`` refers to the current observation number. 

We can generate variables using ``_N`` and ``_n``. An example: if the dataset has 5 observations and we run: 

```
gen var1 = _N
gen var2 = _n
```

then, ``var1`` will equal 5 for all observations while ``var2`` will equal 1 for the first observation, 2 for the second, 3 for the third, and so on. 

We called ``_n`` the **current** observation number because it delicately depends on the current sorting order of the dataset. So, if you use ``_n`` to create another variable (such as creating an ID variable), sort your dataset on a unique combination of variables before setting the ID variable equal to ``_n``.

This is a good place to introduce indexing in Stata. We can use ``[]`` alongwith variable name to do this. For example: ``gen first_obs = total_covaxin[1]`` creates a variable ``first_obs`` that equals a constant value: the value of ``total_covaxin`` for the first observation in the dataset. 

Since ``_n`` refers to the current observation number, it can be used to index by row numbers. For example, ``[_n-1]`` will refer to the observation before the current one; for the second observation, ``[_n-`]`` will equal 2 - 1 = 1, and so will refer to the first observation. So, running ``gen total_covaxin_prev = total_covaxin[_n-1]`` will create a variable that equals ``total_covaxin`` of the previous observation. Note that ``total_covaxin_prev`` is missing for the first observation, which is because Stata doesn't have a "0" observation to refer to when ``_n`` equals 1. 

