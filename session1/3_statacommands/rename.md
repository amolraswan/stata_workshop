---
layout: default
title: rename
nav_order: 8
parent: Stata Commands
grand_parent: Session 1
has_children: false
---

## ``rename``

On the face of it, this is one of the easiest and most boring commands. To rename the variable, run ``rename oldname newname``. But this command has its bag of tricks. Access the help file for ``rename group`` to take a look (``help rename group``). Some of the prominent ones:

- Instead of running ``rename`` on separate lines for two variables, you can run it at once:

```
rename (oldname_var1 oldname_var2 ...) (newname_var1 newname_var2 ...)
```

- Don't like upper case letters in your variable name? To convert variable names to lower case:

```
rename oldname_var1 oldname_var2 ..., lower
```

To convert everything to uppercase, use the option ``upper`` instead of ``lower`` above.

- The best use I have found is the ability to use wildcard characters to remove/add prefixes or suffixes from/to variable names. For example, we currently have ``date_day``, ``date_month``, and ``date_year`` variables in the dataset. Suppose you want to remove the "date_" bit from the names in one go:

```
rename date_* *
```

Stata first identifies variables starting with "date_". ``*`` acts as a stand-in/wildcard for whatever letters come after "date_". In this, ``*`` stands for day, month, or year. And so, Stata accordingly renames the three variables. 

Suppose we want to remove the prefix date\_ and add a suffix \_date to these variable names:

```
rename date_* *_date
```
