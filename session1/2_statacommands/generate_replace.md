---
layout: default
title: generate and replace
nav_order: 7
parent: Stata Commands
grand_parent: Session 1
has_children: false
---

We are finally equipped with enough tools to learn about creating and changing variables!

## ``generate``

The command creates a new variable according to the specified condition. For example, lets create a variable for total doses administered in the covid vaccination data.

```
generate total_doses = male_vac + female_vac + trans_vac
```

Note the ``=`` sign instead of ``==`` used here. Whenever we assign value to a variable, either through ``generate`` , ``replace``, ``recode`` or ``egenerate`` (to be covered in future sessions), we use ``=``. ``==`` is used in conditional statements. ``=`` is the assignment operator while ``==`` is the equality operator.

Stata does not allow the user to overwrite existing variables with the ``generate`` command. If you run the above code twice, Stata will give an error the second time. 

We can also use if-conditional statements with ``generate``. An example:

```
generate date_month_english = "january" if date_month == 1
```

``date_month_english`` will equal january for the observations where ``date_month == 1``, and will be missing for the rest.

## ``replace``

The command edits the values of an existing variable according to the specified condition. The syntax is similar to ``generate``. Continuing our example for the ``date_month_english`` variable:

```
replace date_month_english = "february" if date_month == 2
replace date_month_english = "march" if date_month == 3
replace date_month_english = "april" if date_month == 4
```

Imagine having to do this for all 12 months! There are more efficient and "cooler" methods but we contend with the straightforward way for now. 

We can use the following mathematical operations in ``generate`` and ``replace``: + for addition, - for subtraction, * for multiplication, / for division, ^ for raising to power, log() for natural logarithm, exp() for exponential, etc.

### Plug for ``count``

``count`` returns the number of observations that satisfy the given condition. Running 

```
count
```

returns the total number of observations.

Running

```
count if date_month == 2
```

returns the number of observations from February (date_month ==2)

When you are done creating a variable using ``generate`` and ``replace``, you can run ``count if mi(variable)`` to check if it has any missing values and compare that with what you expected. Sometimes, we fail to cover all the conditions, and so, doing this count can save a lot of trouble. If it is a categorical variable, can also use the ``tabulate`` commmand with the ``missing`` option specified.

