---
layout: default
title: By by
nav_order: 6
parent: Session 3
has_children: false
---

### Basics

``by:`` tells Stata to repeat a given command for each group of observations where the groups are defined by a variable list. Its syntax is: ``by varlist: command``. Stata demands that the data be sorted on the variable list before running ``by``. So, you can either use ``sort`` + ``by:`` or the composite command ``bysort:``. ``bysort:`` really functions the same as ``by:`` except for that it incorporates sorting (so, no need to sort beforehand).

Nick Cox, a Stata legend really, writes on using ``by:`` : "... is one of Stata’s most distinctive and powerful features, but also one that many users find hard to grasp. It is not so much that by: is especially difficult to understand. Rather, the challenge is mainly in absorbing some of the important details, in recognizing when a problem calls for by:, and in thinking your way towards the few lines of Stata that then solve that problem." And he's right on point here!

Lets go through a quick example. We want to summarize ``male_vac`` for each state. We can write a loop for this but specifying the list of states will be tedious (there is, of course, the ``levelsof`` command that eases this but we have not discussed it yet). Anyway, ``by:`` presents the most simple way to do this:

```
bysort lgd_state_name : summarize male_vac

// OR
sort lgd_state_name
by lgd_state_name : summarize male_vac
```

Above, Stata runs the code appearing after the ``:`` for each category of ``lgd_state_name``. 

Similarly, if we want to summarize ``female_vac`` for each day, we can run:

```
bysort date_year date_month date_day: summarize female_vac

// OR
sort date_year date_month date_day
by date_year date_month date_day: summarize female_vac
```

### Creating new variables

As you might anticipate, we can combine ``by`` with ``gen`` or ``egen`` to create new variables. Suppose we want to aggregate our data from district-date level to the state-date level, i.e., we want total vaccination figures at the state level. So, we want to add up the values in each district upto the state level for each day. There are two parts to this task. What comes before ":" -> which tells Stata what variables to sort on and which to aggregate on. And then what comes after ":" -> which tell Stata what command to implement. For the first part, we could write ``bysort lgd_state_name date_year date_month date_day : ``. The second part is not always obvious because you need to know what command and function to use. In this case, we would use the ``total()`` function from the ``egen`` command. So, we could do one of the following:

```
bysort lgd_state_name date_year date_month date_day: egen female_vac_state = total(female_vac)

// OR
sort lgd_state_name date_year date_month date_day
by lgd_state_name date_year date_month date_day: egen female_vac_state = total(female_vac)

```

Importantly, the dataset will not be transformed at the state-date level. We will continue having district-date level data and the variable ``female_vac_state`` will have duplicate values across districts for each day. You can use the ``duplicates drop`` with the appropriate list of variables to get state-date level data (you don't have to!).

### Sort on some, subset on others

We often encounter the need to implement a command within a group (``by``) but the groups need to be ordered internally by another layer of variables (``sort``). Let us motivate this with an example. Suppose we want to create a district ID. The data already has a state ID variable ``lgd_state_id``. We can (1) order districts alphabetically within each state, (2) assign them a number, and (3) create the final district ID by combining district numbers with ``lgd_state_id``. So, it would look like #-% where # is the state ID and % signfies the district's alphabetical order (among that state's districts). Steps 1 and 2 would be accomplished with ``by``. 

Lets first create a dataset of states and their districts by dropping duplicates in districts.

```
keep lgd_state_id lgd_state_name lgd_district_name
duplicates drop 
```

We want to use the current observation ``_n`` to assign numbers to districts witin states. Since we need to have a pre-defined order of districts, we can alphabetically order them up. But when we generate the order variable (``distict_order`` below), we want to subset the ``generate`` command only at the state level. So, steps 1 and 2 can be accomplished by:

```
sort lgd_state_name lgd_district_name
by lgd_state_name: generate district_order = _n
``` 

Lets deep dive into what we are doing here. We first sorted the data by state and district names. Then for each state, we told Stata to generate a variable ``district_order`` that equals the observation number within that state. Since each observation refers to a particular district and they are arranged alphabetically, the resultant ``district_order`` value accomplishes steps 1 and 2. 

The pertinent question is how to do this using ``bysort``. It's a neat syntax trick. We first specify all the variables which are used in both ``sort`` and ``by``. Then we specify the variables used only in ``sort`` within paranthesis ``()``. Look at the code below:

```
// this does the exact same thing as the separate sort and by code chunk above 
// lgd_district_name in () signifies that it's only a sorting variable and not a "by" variable
bysort lgd_state_name (lgd_district_name) : generate district_order = _n
```

For completeness' sake, let us also implement step 3 though we are jumping the gun here. ``lgd_state_id`` is already a string variable; it contains numbers but is stored as a string variable. We want the same for our ``district_order`` variable and can do that using ``tostring``. Then, we just combine the two string variables, separated with a hyphen:

```
tostring district_order, replace // convert district variable to string

// creating district ID variable by combining strings. can combine strings by simply using the + operator 
generate lgd_district_id = lgd_state_id + "-" + district_order

```

Voila!

It takes time, practice, and experience with different problems to develop expertise in ``by``. I am certainly not an expert in it but [this article](https://www.stata-journal.com/article.html?article=pr0004) by Nick Cox is a step in the right direction. It's full of examples, highly recommended!