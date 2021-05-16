---
layout: default
title: Stored results
nav_order: 4
parent: Session 2
has_children: false
---

Question 1 of sessions 1's assignment required us to use the mean and standard deviation of the variables to construct their standardized versions. The way we did it then was to run the summarize command, look at the mean and standard deviation, and run a version of the following command: ``gen total_covaxin_stan = (total_covaxin - ###)/###``. Here ### refer to whatever the values of its mean and standard deviation were. However, this process will breakdown if we got another 100 observations to the dataset or if we corrected a few errors in the ``total_covaxin`` variable. Why? Because then we'd have to manually re-check the mean and standad deviation, and edit the ### values accordingly. Easy to do for one variable, but annoying, error-prone, and time-consuming when you have to input multiple values as in Q1.b. 

Many Stata commands such as ``summarize``, ``count``, ``regression``, etc. store their results in the memory for easy access -> all to mean that what we see in the output can be accessed "programmatically". For example, ``summarize`` stores the variable mean in ``r(mean)``. So, we can run the following to display the mean of the ``total_covaxin`` variable.

```
summarize total_covaxin
di `r(mean)'
````

Though I used `` `' `` around r(mean), it is necessary only in a few situations, the most important one being when you want to access r(mean) in a string, such as:

```
summarize total_covaxin
di "the mean of total_covaxin is `r(mean)'"
```

Going back to the standardization example, we can run something like:

```
summarize total_covaxin
gen total_covaxin_stan = (total_covaxin - `r(mean)')/`r(sd)'
```

Here, we used ``r(sd)`` to refer to standard deviation. To see the complete list of stored results for a command, either check the last section of the command's help file or after running the command, run ``return list``. 

Stored results stay in the memory for as long as we don't run another command that stores results. We can use local macros to store these stored results for later use. An example:

```
summarize total_covaxin
local covaxin_mean `r(mean)'
summarize total_covishield 
local covishield_mean `r(mean)'

di "total_covaxin variable's mean is `covaxin_mean' "
di "total_covishield variable's mean is `covishield_mean' " 
```

Stored results come in four classes. Two most common are r() and e(). We will not discuss these in detail now and I encourage you to refer to this [page](https://stats.idre.ucla.edu/stata/faq/how-can-i-access-information-stored-after-i-run-a-command-in-stata-returned-results/) for more details. 
