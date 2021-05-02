---
layout: default
title: drop and keep
nav_order: 6
parent: Stata Commands
grand_parent: Session 1
has_children: false
---

## ``drop`` and ``keep``

``drop`` and ``keep`` have similar syntax but the polar opposite objectives. They both can be applied in two different ways:

- ``drop variable1 variable2 ...`` deletes the listed variables. ``keep variable1 variable2 ...`` keeps the listed variables and deletes the rest. 
- ``drop if ...`` deletes observations that satisfy the conditional statement. ``keep if ...`` keeps the observations that satisfy the conditional statement and deletes the rest.

In the first case, we drop/keep certain "columns" in the dataset. In the second case, we drop/keep certain "rows" in the dataset. Ensure that you understand the difference. If you do, you will realize that ``drop variable1 if variable2=="something"`` does not make sense. The conditional statement takes us to the second case, so Stata thinks we want to delete the observations for which variable2 equals "something". But then we are telling it to drop variable1 which takes us to the first case; there cannot be a conditional statement on values of other variables in the first case. 

If the idea is to replace the values of variable1 to missing if variable2 equals "something", we need to use the ``replace`` command which is covered below. 

