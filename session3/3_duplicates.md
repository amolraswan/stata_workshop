---
layout: default
title: Duplicates!
nav_order: 3
parent: Session 3
has_children: false
---

Duplicates are observations with identical values on a given list of variables. It is important to spot them and then rectify or drop them from the dataset. ``duplicates`` command helps us accomplish this. It has a few subcommands such as ``report``, ``tag``, ``list``, ``drop``, and ``examples``. The way to use them is by combining the main command with the relevant sub-command: ``duplicates report``, ``duplicates tag``, ``duplicates list``, ``duplicates drop``, and ``duplicates examples``. 

Lets define "proper" duplicate observations as ones that have identical values on all variables and "improper" duplicate observations as ones that have identical values on atleast one but not all the variables. This distinction is non-standard but essential: if you want to drop duplicates (i.e., if 2 observations are duplicates, you want to drop one of them), dropping "proper" duplicates is _okay_ whereas dropping "improper" duplicates requires thinking about why they are identical on some but not all the variables. Of course, once we can confirm the reason, it's okay to drop "improper" duplicates. We will come back to this.

We will use a sample Stata dataset to illustrate the basics of the duplicates command. For this, we will follow a Stata help file example. The dupxmpl dataset has 3 variables: ``id``, ``x``, and ``y``. It has 198 unique observations and 4 duplicate observations (2 copies of each observation). We can get these numbers using the ``duplicates report`` command.

```
// Using a sample dataset stored on Stata's servers
use https://www.stata-press.com/data/r13/dupxmpl 
// could have also used the webuse command: webuse dupxmpl

duplicates report 
```

Since we have few duplicates and not a lot of variables, we can use the ``duplicates list`` command to view them. However, usually, we want to mark duplicates and then ``rowse`` them. ``duplicates tag`` command allows us to create a variable that tracks duplicates and then we can browse conditional on this variable's values. Example below:

```
// simply listing the duplicates
duplicates list 

// browsing the duplicates
duplicates tag, gen(dup)
br if dup >= 1 
```

Be wary of the ``dup`` variable. It equals 0 for unique observations, 1 for a pair of duplicate observations (so an observation in such a pair has "1" duplicate), 2 for a trio of duplicate observations (so an observation in such a trio has "2" duplicates), and so on.

In the above examples, we did not specify what variables to consider; so Stata used all the three variables: ``id``, ``x``, and ``y``. Hence, the duplicates we found were "proper" duplicates. We can drop them by using the ``duplicates drop`` command:

```
duplicates drop // dropping the "proper" duplicates
```

Lets move on to "improper" duplicates. For this, we return to our covid-vaccination dataset. Suppose you want to save a dataset with state and district names -> something like a directory. Given that the dataset is at district-day level, we will have duplicates in the states-districts, i.e., duplicates in ``lgd_state_name lgd_district_name``. We can inspect this by supplying the list of variables to Stata.

```
// load the covid vaccination data
duplicates tag lgd_state_name lgd_district_name, gen(dup) 
tabulate dup
```

While we have duplicates in states-districts, we do not have duplicates in states-districts-dates. Focus on this statement. Once we include ``date`` in the list of variables to check duplicates on, each observation gets a unique combination of state-district-date, and therefore, all observations are unique. 

Anyway, suppose we want to drop the duplicates in states and districts. ``duplicates drop`` command requires the user to specify the ``force`` option if they want to drop duplicates on a list of variables. This is meant as a safeguard against the user's stupidity I guess; there has to be a better reason than that though but for now lets accept that Stata wants the ``force`` option to ensure that the user understands that dropping "improper" duplicates is a tricky business. In our case, we know why there are duplicates and why it is okay to drop them. So, we can run:

```
duplicates drop lgd_state_name lgd_district_name, force

```

But before you save the resultant dataset, take a look at other variables. Since the original dataset recorded vaccination numbers at the district-day level, the vaccination variables don't make any sense now. So we want to keep only the relevant variables -> ones that make sense at the district level. In this special case, we wanted to create a directory dataset of state and district names, so lets keep those variables:

```
keep lgd_state_name lgd_district_name

```

Again, in this very special case of wanting to create a directory, it would have made sense to drop the irrelevant variables before dropping the duplicates. In this way, we would have dropped "proper" duplicates because the dataset would have contained only two variables - state and district - and so the ``duplicates drop`` command could have been run without specifying a list of variables.
