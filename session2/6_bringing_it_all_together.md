---
layout: default
title: Bringing it all together
nav_order: 6
parent: Session 2
has_children: false
---

We can now accomplish objective #2 which was to have an efficient code for session 1's assignment Q1.b. 

Lets focus on one variable: ``total_covaxin``. We want to summarize it and use the stored results on mean and standard deviation to create a new standardized variable, all the while ensuring to use month-specific statistics. 

For a single month, say March, we'd do this: (skipping the part where we generate an empty standardized variable)

```
summ total_covaxin if month == 3
replace total_covaxin_stan2 = (total_covaxin - `r(mean)')/`r(sd)' if month == 3
```

We don't want to repeat this step for each month, so we use a ``forvalues`` loop.

```
gen total_covaxin_stan2 = .
forvalues month = 1/4 {
	summ total_covaxin if month == `month'
	replace total_covaxin_stan2 = (total_covaxin - `r(mean)')/`r(sd)' if month == `month'
}
```

Q1.b required us to do this for three variables: ``total_covishield``, ``total_covaxin``, and ``female_vac``. We can write similar code as above for the other two variables or we can put all this in another loop that goes through each variable. So, this will mean having two loops: the outer loop going through each variable and the inner loop going through each month. 

```
local var_for_stan "total_covishield total_covaxin female_vac"
foreach var of local var_of_stan {
	gen `var'_stan2 = .
	forvalues month = 1/4 {
		summ `var' if month == `month'
		replace `var'_stan2 = (`var' - `r(mean)')/`r(sd)' if month == `month'
	}
}
```

We are done!

This was an extremely challenging session, not helped at all by the fact that it was just the second day. But now that we are through with it, you will have time to practise and make yourself comfortable with macros and loops. More to discuss in the next session!