---
layout: default
title: Local macros
nav_order: 3
parent: Session 2
has_children: false
---

The essential function served by local macros is similar to global macros: to store values. However, global macros stay in the memory long after their execution whereas local macros are dropped after the code is executed (when working in do-files). In most cases, we do not need the value beyond a particular chunk of code and so, it is advisable to use local macros. More importantly, global macros can cause conflicts when you are working across multiple do-files. Since we need file paths throughout and across do-files, file paths can be saved in global macros. 

Another difference arises in the coding. To create a local macro, we use the ``local`` command, to reference it, we use `` ` ' ``.

A local macro is, therefore, a box that equals an element (i.e., single-valued) or is a list of elements. Lets start with setting up a single-valued local macro, which follows a similar code as for the global macros we set up previously. An example:

```
local x 7 // setting up a local macro, x that equals 7
di `x'

local y "pepsi" // setting up a local macro, y that equals "pepsi"
di "`y'" // enclosing `y' in "" because it equals a string
```

To define a local as a list of elements, simply separate the elements with a single space. An example:

```
local y_multiple "pepsi coke sprite"
di "`y_multiple"
```

At this stage, ``y_multiple`` can be seen both a single-valued local that equals "pepsi coke sprite" or a local containing a list of names: "pepsi", "coke", and "sprite". The latter is useful in for-loops which we will cover shortly. Before this, lets see some examples of how to use locals.

- A silly example of how to use a local inside a string. 

```
local x 7
di "we defined the local macro x to equal `x'"
```

- Suppose you want to count the mean number of females who got vaccinated in Tamil Nadu. We can do this:

```
local state "tamil nadu"
summ female_vac if lgd_state_name == "`state'"
// can check the mean
```

In both examples, Stata sees `` `' `` and realizes that we are using a local. It then finds that local and inputs its value in the expression. In the second example, it sees `` `state' `` and inputs `` tamil nadu`` in the `` "" ``. 