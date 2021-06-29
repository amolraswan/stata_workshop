---
layout: default
title: Variable Documentation
nav_order: 3
parent: Session 4
has_children: false
---

### Variable Labels

Like a book is about much more than its cover, variables can also not be described fully by their names. This necessitates variable labels that help in conveying important information about the variable. You can see these in the "Variables" window, next to the variable names. ``describe`` outputs a table containing variable labels as well. FOr example, we have two district variables in the data ``lgd_district_name`` and ``district``. The label for ``district`` clarifies that it is the "district name from COWIN dashboard". Super important!

Assigning variable labels is easy. The command is ``label variable`` which can be shortened to ``la var`` (I often write ``label var`` but it really depends on the mood haha). The syntax is ``label var variable_name "variable label"``. For example, we don't have variable labels for ``date_day``, ``date_month``, and ``date_year``. We could label them as follows:

```
label var date_day "Day"
label var date_month "Month"
label var date_year "Year"
```

### Value Labels

Stata allows to label values of a numeric variable which is useful for categorical variables such as sex, education, marital status, etc. 

Labelling values is helpful in storing valuable information about what category is implied by a particular number so that the user doesn't always have to go through the do-file to check and because output of several commands (like ``tabulate``) displays the labels instead of numbers. One could store such categorical variables as string variables but that increases the dataset size non-trivially and impedes the use of those variables in the ``regression`` command since it accepts only numeric categorical/factor variables.

For example, you might have an education variable that equals 0 for no education, 1 for high school, 2 for bachelor's degree, 3 for master's degree, etc. We can store this as a numeric variable and assign value labels to the numbers as per the definitions. So, 0 would be displayed as "no education", 1 as "high school", 2 as "bachelor's degree", 3 as "master's degree", etc. Internally, Stata stores numeric values and knows what numbers correspond to what labels -> storing numeric values for the observations helps in reducing the memory it would have otherwise taken to store a string variable. 

Labelling a variable has two steps: (1) defining a value label and (2) assigning it to a variable. We have a separate step for defining a value label because several variables can have the same categories, such as variables that record responses to yes-no questions. We define a label using ``label define`` and assign it to a variable using ``label values``. 

Syntaxes are ``label define label_name # "label" ## "label" ...`` and ``label values variable_name label_name``. Lets illustrate with an example:

```
// creating value label called "yesno"
// 1 -> yes, 0 -> no, -66 -> don't know
label define yesno 1 "yes" 0 "no" -66 "don't know" 

// lets assign the "yesno" label to a variable called love_plants
label values love_plants yesno

// can assign the "yesno" label to multiple variables at the same time as well
// suppose we have 3 variables love_plants love_animals love_humans
label values love_plants love_animals love_humans yesno
```

We defined above "yesno" label for 3 categories - yes, no, and don't know. Suppose we later discover that there was a fourth response "don't want to answer" which was input as -99. We can add it to the existing label by using the option ``, add``. We can change the existing # to label correspondences using the ``, modify``. An illustration:

```
// adding "don't want to answer" correspondence to "yesno" label
label define yesno -99 "don't want to answer", add
```

You can list a particular value label using ``label list label_name``. To check if a variable has a value label attached, we can use the ``describe`` or ``codebook`` command. We can also select a variable in the "Variables" window and then check in the "Properties" window if the variable has a value label. As mentioned previously, variables displayed in blue while browsing the data signify that it is a numeric variable with value labels (instead of being a string variable). 

[This](https://wlm.userweb.mwn.de/Stata/wstatlab.htm) and [this](https://stats.idre.ucla.edu/stata/modules/labeling-data/) are good primers on variable and value labels.