---
layout: default
title: describe, tabulate, and summarize
nav_order: 3
parent: Stata Commands
grand_parent: Session 1
has_children: false
---

As a helpful reminder, we are working on the covid vaccination data and the examples will use variables from this dataset. We will cover three commands in this section: ``describe``, ``tabulate``, and ``summarize``. 

## ``describe``

The command outputs basic information about the dataset, including the number of observations and variables, variables in the dataset, their type, value label, and variable label. It is a versatile command and you can take a look at its help file for different uses. For the moment, you can run the command to get a quick overview of what all variables are present in the dataset, what they mean (if variable labels are provided), etc. Simply run:

```
describe
```

## ``tabulate``

Suppose you want to learn which states are covered in the datasets and the number of observations per state. There are, of course, multiple ways to do this but the one I find the simplest and most useful at a preliminary stage is to run the ``tabulate`` command. It gives you the number of observations for each state (and the corresponding figure in percentage terms). Run:

```
tabulate lgd_state_name
```

There can often be missing values in the variables. ``tabulate`` excludes them from its output. It is recommended to instruct Stata to include them for which you need to add the ``missing`` option. So, run:

```
tabulate lgd_state_name, missing
```

Quite fortunately, there are no missing values in this variable!

Clearly ``tabulate`` is relevant only for categorical variables or continuous variables that have few unique values. For example, it would not make sense to run ``tabulate total_covaxin`` ; in fact, Stata will tell you that the variable has "too many values". 

What we have discussed so far is oneway tabulation, i.e., tabulating the values of a single variable. We can also tabulate two variables together which helps in seeing the relationship between them. We don't really have variables that will illustrate this point well, but as example we can check what days we have for each month in the dataset.

```
tabulate date_month date_day, missing
```

Some people use ``tabulate`` to create dummy/indicator variables, i.e., for each category of the state variable, you can create a separate variable that equals 1 for a given state and 0 for all others. So, the following command would create 37 variables, one variables for one state. 

```
tabulate lgd_state_name, gen(state)
```

Browse part of the resultant data to see how the variables look. Or take a look at the last entries of the variables window. For example, state4 equals 1 for observations from Assam and equals 0 otherwise.

## ``summarize``

The command is to be used for continuous variables, such as income, age, total vaccinations, etc. It presents summary statistics such as mean, median, standard deviation, etc. To give a high-level overview for all eligible variables in the dataset, run:

```
summarize
```

which will output the number of non-missing observations, mean, standard deviation, minimum value, and maximum value for each eligible variable (i.e., the non-string variables). Note that the summary statistics are computed on the non-missing observations; for example, in the computation of mean, the N (number of obs in the denominator) excludes missing observations -> as it should!

You can also run the summarize command for a specific variable (gives the same information):

``` 
summarize total_covaxin
```

To get more information, such as the 10th percentile, median, 95th percentile, kurtosis, etc., add the ``detail`` option:

```
summarize total_covaxin, detail
```

