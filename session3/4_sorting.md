---
layout: default
title: Sorting
nav_order: 4
parent: Session 3
has_children: false
---

I have already mentioned 'sorting' before but haven't defined what it means. Of course, it's not rocket science; sorting means arranging observations in a particular order. In most contexts, this order is either ascending or descending and is defined on the values of a user-defined set of variables. 

Stata has two commands for sorting: ``sort`` and ``gsort``, the only difference between the two being that ``sort`` performs ascending-order sorting only while ``gsort`` performs both descending and ascending-order sorting.

For example, suppose you want to sort your dataset by state and district names in an ascending fashion (i.e., a comes before b, and so on). The statements below are equivalent:

```
sort lgd_state_name lgd_district_name
gsort +lgd_state_name +lgd_district_name
```

The syntax is similar: first the command and then the variables on which we want to sort. In ``gsort`` we add the ``+`` in front of the variable name to indicate that we want to sort ascendingly on that variable. Expectedly, ``-`` refers to descending sorting on a variable. So, the following statement sorts the observations ascendingly on state names but descendingly on district names.

```
gsort +lgd_state_name -lgd_district_name
```

Importantly, the _order_ of the variables in that variable list is important. In ``sort lgd_state_name lgd_district_name``, Stata first sorts on state names and within each state, sorts on district names. So, the sorted data looks like:

| lgd_state_name | lgd_district_name |
|--------|-----------|
| state1 | aaa |
| state1 | aab |
| state1 | bcc |
| ...    | ...       |
| state2 | aac |
| state2 | bbb |
| ...    | ...       |


However, if we were to flip the order of the variables in that list, i.e., we were to run ``sort lgd_district_name lgd_state_name``, then Stata would first sort on district names and within each district, would sort on state names. So, the sorted data would look like:

| lgd_state_name | lgd_district_name |
|--------|-----------|
| state1 | aaa |
| state1 | aab |
| state2 | aac |
| state2 | bbb |
| state1 | bcc |
| ...    | ... |

So, be careful about what you want haha! It's helpful to quickly browse the data after sorting to confirm we did it right.

