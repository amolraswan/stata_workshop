---
layout: default
title: For Loops
nav_order: 5
parent: Session 2
has_children: false
---

In programming, a **for loop** is used to repeat a particular section of code a pre-defined number of times. It is a powerful method to code efficiently. Stata has two commands for "for" loops: ``forvalues`` and ``foreach``. We can use ``forvalues`` for looping over numbers while we can use ``foreach`` for looping over both numbers and string values (such as names of states). 

### ``forvalues``

We start with a rather simple (silly?) example: suppose you want to display numbers 1 to 5. One way would be to write ``display #`` command five times, with # being a different number from 1 to 5 each time. A for loop helps us automate this by asking Stata to run ``display `x'`` for a local macro ``x`` that takes values 1 to 5:

```
forvalues x = 1/5 {
	display "number `x'"
}
```

The ``forvalues`` bit tells Stata which command we want to use. ``x`` is the name of local macro we want to use within the for loop. The name is inconsequential; we could have easily called it ``num``. We then specify the start and end values for the loop in ``1/5``. The commands to be run in the loop go inside curly brackets ``{ ... }`` of which the first one comes at the end of the same line as ``forvalues`` while the second one comes at a separate line at the end.

In another application, we can summarize the ``total_covaxin`` variable for each month using ``forvalues``:

```
forvalues month = 1/4 {
	summ total_covaxin if date_month == `month'
}  
```

### ``foreach``

The basic principle behind ``foreach`` remains the same as for ``forvalues``. There is only a slight change in its syntax. We first define a local macro that is a list of elements over which we want to loop. And then we tell Stata to loop over these elements. For starters, lets repeat the above example but with ``foreach``.

```
local month_list 1 2 3 4
foreach month of local month_list {
	summ total_covaxin if date_month == `month'
}
```

In the line of ``foreach``, ``of local month_list`` tells Stata to refer to a local that's named ``month_list``. There are a few different syntaxes that go with ``foreach`` but we will focus on this one to keep things (relatively) simple. You are encouraged to refer to the command's help file.

Now, we look at a situation where we want to loop over string values. Lets say we are interested in summarizing the ``total_covaxin`` variable for the states of kerala, punjab, haryana, and assam. It'd look like this:

```
local state_list "kerala punjab haryana assam"
foreach state of local state_list {
	summ total_covaxin if lgd_state_name == "`state'"
}
```

If we want to add "tamil nadu" to the ``state_list`` macro, we need to be careful that Stata recognizes it as a phrase. Writing ``local state_list "kerala punjab haryana assam tamil nadu"`` is incorrect because Stata will interpret "tamil" and "nadu" as distinct elements. Instead, we need to write "tamil nadu" in double quotes, so something like: ``local state_list "kerala punjab haryana assam "tamil nadu""``.


We can also use ``foreach`` and ``forvalues`` to fill in variable names. As a silly example, suppose you want to multiply each of the following variables by 2: ``male_vac``, ``female_vac``, and ``trans_vac``. You can either do this separately for each variable or use a ``foreach`` loop:

```
local var_name_list "male_vac female_vac trans_vac"
foreach var of local var_name_list {
	replace `var' = `var'*2
}
```

Importantly, though these are strings, note that when we refer to variables, we don't put the local macro ``var`` in double quotes, instead, we write `` `var' ``. This is to let Stata know that we are referring to variable names in the dataset. In this special case, the three variables have a common suffix ``_vac``, so we could have alternatively written:

```
local var_name_chunk "male female trans"
foreach var of local var_name_chunk {
	replace `var'_vac = `var'_vac*2
}
```