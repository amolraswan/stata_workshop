---
layout: default
title: Primer on Stata Commands
nav_order: 1
parent: Session 1
has_children: false
---

# Primer on Stata Commands

### Command Structure 

Most commands in Stata follow this structure:

```
command variable1 variable2 , option1 option2 ...
```

or 

```
command ... filename, option1 option2 ...
```

Examples of the first type are ``tabulate age sex`` , ``tabulate age sex, missing``, and ``summarize income``. Of the second type: ``sysuse auto``, ``sysuse auto, replace``, and ``merge id using random.dta``. Don't worry about what these commands do, we will look at them below.

Stata is not the grandparent who mistakes LOL for "Lots of Love", but is the hipster nerd who uses FWIW for "For what's it worth". Well, all to say that Stata is smart enough to understand that we mean ``tabulate`` when we only type ``tab``. So, ``tab age sex`` is equivalent to ``tabulate age sex``. Similarly, it is okay to just write ``summ`` instead of ``summarize``. It essentially understands what command we mean by finding a unique match for the first # letters. The help file of a command tells us how many first letters we need to type out. More on accessing and understand the help file later. (If you are super curious, type ``help tabulate`` to access the help file for the ``tabulate`` command). 
