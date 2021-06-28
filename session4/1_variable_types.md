---
layout: default
title: Variable Types
nav_order: 1
parent: Session 4
has_children: false
---

Variables are, broadly, either numeric or string (text). The terms are quite self-explanatory; numeric variables contain numbers such as integers, decimals, etc. while string variables contain text such as names, addresses, etc. If you think about it, numbers are text and so, it can happen that string variables are composed entirely of numbers. In our dataset, the ``date`` variable is an example of this; it is just numbers but stored as a string. (we'll see below how to tell Stata to store it as a numeric variable though this is not _really_ needed here)

Numeric variables can be stored as byte, int, long, float, or double. We don't need to know the differences between these now, except that float and double types can hold decimal values. We don't have to explicitly instruct Stata which of these to use; it figures it out automatically.

Thankfully, string variables have their lives sorted and their _sub-types_ just signify the maximum string length of an observation.For example, if the longest name in a variable is "toolazytosetanamewow", then this variable will be stored as "str20" where 20 tells us the max string length. 

For more details on these, you can read [this](https://povertyaction.github.io/guides/cleaning/variablemanagement/storagetypes/) and [this](https://povertyaction.github.io/guides/cleaning/06%20Coding%20in%20Stata/02%20Numerical%20Formats/). We haven't discussed dates in Stata but the first page discusses them briefly (happy reading!). 

In case a string variable contains only numbers ("numeric characters"), you can convert it into a numeric variable using the ``destring`` command. As mentioned above, ``date`` variable is an example. We just run the following to change its type to numeric:

```
destring date, replace
```

On the other hand, we can convert a variable's type from numeric to string using the ``tostring`` command. This can come in handy when combining different numeric IDs to create a single ID, as in [the last example here](https://amolraswan.github.io/stata_workshop/session3/6_by/). A simple example:

```
// asssuming you converted date to numeric above
tostring date, replace
```

