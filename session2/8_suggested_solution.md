---
layout: default
title: Suggested solutions
nav_order: 8
parent: Session 2
has_children: false
---

These are only suggestions and sans any formatting!

- Question 1:

```
local sum_0_49 = 0 // initiating the sum at 0
forvalues x = 0/49 {
	local sum_0_49 = `sum_0_49' + `x'
}
di `sum_0_49' // 1225!
```

- Question 2:

```
local period_list "day month year"
foreach var of local period_list {
	rename date_`var' `var'
}
```

- Question 3:

```
local var_rename "male female trans"
foreach var of local var_rename {
	rename `var'_vac total_vac_`var'
}
```

- Question 4:

```
// a. storing means in locals
forvalues x = 1/31 {
	summ total_covishield if month == 3 & day == `x'
	local mean_on_`x'_march `r(mean)'
}

// b. displaying the locals
forvalues y = 1/31 {
	di "Mean covishield vacc on `y' March were: `mean_on_`y'_march' "
}
```