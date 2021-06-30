---
layout: default
title: Combining Data - Append
nav_order: 4
parent: Session 4
has_children: false
---

``append`` helps us add rows (observations) to the existing dataset. Intuitively, this means that we have data on the same variables for different sets of people (or any observed unit, such as day, district, country, etc.) stored in different files; and we want to combine these together -> this takes the form of stacking data below each other. 

The syntax is simple: ``append using using_data`` where ``using_data`` is the data to be appended. The dataset already present in memory is called master dataset. For example, we may have math test scores for three sections of class 10th of a school - section A, B, and C - in three files (``test_score_A.dta``, ``test_score_B.dta``, and ``test_score_C.dta``). Then:

```
// lets import test scores for section A first
use "test_score_A.dta", clear

// appending test scores for section B and then section C
append using "test_score_B.dta"
append using "test_score_C.dta"

// DONE!
```

Contrary to popular belief, you don't need to start with a dataset loaded into the memory. That is, you can start with no data and then keep appending. This comes in super handy during loops:

```
clear all // no data in memory

append using "test_score_A.dta"
append using "test_score_B.dta"
append using "test_score_C.dta"

// we can do this in a loop as well.
clear all // starting with a clean slate

foreach x in A B C {
	append using "test_score_`x'.dta"
}
```

There are a few important things to consider in this otherwise easy commmand:

- The above appending process could end up being flawed if we don't have a variable identifying different class sections. We can either ensure it's there already or add it while appending:

```
clear all // starting with a clean slate

foreach x in A B C {
	append using "test_score_`x'.dta"
	if "`x'" == "A" {
		gen section == "A"
	}
	else {
		replace section == "`x'" if mi(section)
	}
}
```

- Be careful about variable types across the master (already in memory) and using data (to be appended). If a variable is string in one and numeric in the other, Stata will stop the append process and issue an informative error message telling you which variable has this issue. The ``force`` option is a way out that tells Stata to ignore this complication. BUT you should almost NEVER specify ``force`` because Stata will drop the values of that variable from the using data. Instead, figure out if the variable should be string or numeric, and convert it accordingly in the relevant data before appending (``destring``, ``tostring``). For example, if test scores were inadvertently imported as string variable in ``test_score_A.dta``, one could ``destring`` them before appending section B and C data. 

- 
I strongly recommend reading the "Remarks and Examples" section of the Stata ``append`` [documentation](https://www.stata.com/manuals/dappend.pdf). Make sure to not just read but also to implement these suggestions/tips!