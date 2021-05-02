---
layout: default
title: Conditional Statements
nav_order: 4
parent: Stata Commands
grand_parent: Session 1
has_children: false
---

What if we want to know the number of vaccinations done on April 2 or the average number of daily covishield vaccinations done in March in Pathankot, Punjab (which is my hometown!)? 

## If qualifier

We can use the ``if`` qualifier with our commands to get the relevant numbers for particular group of observations. Important: I called it a "qualifier" and not a "command" because it helps subsets/qualifies certain observations for further use in a Stata command. Lets compute the average, district-wise number of daily covishield vaccinations done in March throughout India:

```
summarize total_covishield if date_month == 3, detail
```

It looks like the average number of daily covishield vaccinations in a district was 35486 in March. The distribution is quite spread out. The 5th percentile is 2161 whereas teh 95th percentile is over 1,00,000. Of course, these figures haven't been normalized for district population, i.e., looking at absolute number of vaccinations does not take into account that vaccinations could be lower for districts with lower populations.

Anyway, lets get back to what we ran. The additional piece is ``if date_month == 3``. We are telling Stata to only consider data from the month of March. Also note that the ``, option1 option2 ...`` segment of the code comes after the 'if statement' and not before. 

## And/Or

What if you want to now look at the average daily vaccinations in Punjab's districts in March? That is, instead of all Indian districts, we want to restrict the sample to Punjab districts. So, we now have two statements we want to subset on: ``date_month == 3`` and ``lgd_state_name == "punjab"``.
Sorry my markdown (tool in which this webpage is written) skills are still not great enough, so you will need two sets: set of all observations with ``date_month == 3`` and another set of observations with ``lgd_state_name == "punjab"``. Do we want an intersection or a union of these sets? 

An intersection! We want to look at the data pertaining to Punjab districts in March. An intersection means "and", i.e., both the conditions should be satisfied. Stata does not understand the english word "and", instead we need to use "&". So, how will our if statement look? ``if date_month == 3 & lgd_state_name == "punjab"``. So, we run:

```
summarize total_covishield if date_month == 3 & lgd_state_name == "punjab", detail
```

For completeness, let's come back to the question posed at the top. Try figuring out how you would do it. 

What I'd try: First tabulate Punjab districts to check the capitalization and spelling of Pathankot and then run the actual command.

```
tab lgd_district_name if lgd_state_name == "punjab"
summarize total_covishield if date_month == 3 & lgd_state_name == "punjab" & district == "pathankot", detail
```

Lets move on to 