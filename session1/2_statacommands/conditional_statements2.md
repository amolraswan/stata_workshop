---
layout: default
title: Conditional Statements II
nav_order: 5
parent: Stata Commands
grand_parent: Session 1
has_children: false
---


## ``<=, <, >, >=, !=, missing()``

So far, we have dealt with the equality condition ``==``. The expression for "less than or equal to" is ``<=``, "strictly less than" is ``<``, "strictly more than" is ``>``, and "more than or equal to" is ``>=``. ``!=`` stands for "not equal to".

One short example: Instead of looking at the whole month of March, lets take a look at average daily covishield vaccinations at district level (all India sample) for:

1. the first 15 days of March 

```
summarize total_covishield if date_month == 3 & date_day <= 15
```

2. between 16 and 25 March 

```
summarize total_covishield if date_month == 3 & (date_day >= 16 & date_day <= 25)
summarize total_covishield if date_month == 3 & inrange(date_day, 16, 25)
```

3. 26 through the end of March

```
summarize total_covishield if date_month == 3 & (date_day >= 26 & date_day <= 31)
summarize total_covishield if date_month == 3 & inrange(date_day, 26, 31)
summarize total_covishield if date_month == 3 & date_day >= 26
summarize total_covishield if date_month == 3 & date_day >= 26 & !missing(date_day)
```

Lots of heavy stuff happening in #2 and #3 above. Lets unpack:

- ``inrange(variable, lower value, upper value)`` is an alternative to writing ``variable <= lower value & variable >= upper value``
- In #3, since we know we need to go from March 26 to March 31 and there are no days beyond 31 (always a good idea to verify this in the data!), we can skip the ``date_day <= 31`` bit. This is what I do in the third line of the code. *Super important*: Missing values in Stata are essentially infinity, so higher in value than non-missing values. What does this mean? If there are any missing values in the date_day variable, writing just ``date_day >= 26`` will include them -> which we do not want! So, if you don't want to define the upper limit but want to exclude missing observations of the date_day variable, *always* include the ``!missing(date_day)`` bit in your code -> which is what we do in the fourth line.  

Sometimes, we want to condition on the missing values of a certain variable because this can give us valuable information about observations that do not have any value for that variable. In this case, our statement would look like ``if missing(variable)``. An often used shorthand for ``missing()`` is ``mi()``.

There is another way to identify missing values in Stata. Missing values for string variables are empty strings, so, for a missing state name, ``mi(state)`` and ``state == ""`` are equivalent. Missing values for numeric variables are much more complicated but you will typically not be dealing with the more complicated cases. Mostly, missing values for numeric values are represented by a dot ``.``. So, for a missing value of age, ``mi(age)`` is roughly equivalent to ``age == .``. Note that in 99.99% cases (I don't have data to back this claim though), these are equivalent! They are not equivalent when the data contains extended missing values which are a way of differenting between reasons for missing values. These are .a, .b, ... , .z. For example, a survey may code a missing value in income as ``.d`` if the respondent does not know the answer and as ``.r`` if the respondent refuses to answer. In this case, ``mi(income)`` identifies both the cases whereas ``income == .`` will identify none. You could alternatively write ``income == .d`` or ``income == .r`` as per what you desire to condition. For more details on extended missing values, refer [here](https://povertyaction.github.io/guides/cleaning/variablemanagement/missingvalues/#extended-missing-values-in-stata).

