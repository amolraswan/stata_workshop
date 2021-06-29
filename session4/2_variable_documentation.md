---
layout: default
title: Variable Documentation
nav_order: 3
parent: Session 4
has_children: false
---

Like a book is about much more than its cover, variables can also not be described fully by their names. This necessitates variable labels that help in conveying important information about the variable. You can see these in the "Variables" window, next to the variable names. ``describe`` outputs a table containing variable labels as well. FOr example, we have two district variables in the data ``lgd_district_name`` and ``district``. The label for ``district`` clarifies that it is the "district name from COWIN dashboard". Super important!

Assigning variable labels is extremely easy. The command is ``label variable`` which can be shortened to ``la var`` (I often write ``label var`` but it really depends on the mood haha). The syntax is ``label var _variable_ "variable label"``. 