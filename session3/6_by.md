---
layout: default
title: By by
nav_order: 6
parent: Session 3
has_children: false
---

``by:`` tells Stata to repeat a given command for each group of observations where the groups are defined by a variable list. Its syntax is: ``by varlist: command``. Stata demands that the data be sorted on the variable list before running ``by``. So, you can either use ``sort`` + ``by:`` or the composite command ``bysort:``. ``bysort:`` really functions the same as ``by:`` except for that it incorporates sorting (so, no need to sort beforehand).

Nick Cox, a Stata legend really, writes on using ``by:`` : "... is one of Stata’s most distinctive and powerful features, but also one that many users find hard to grasp. It is not so much that by: is especially difficult to understand. Rather, the challenge is mainly in absorbing some of the important details, in recognizing when a problem calls for by:, and in thinking your way towards the few lines of Stata that then solve that problem." 

Lets go through a quick example. We want to summarize ``male_vac`` for each state. We can write a loop for this but specifying the list of states will be tedious (there is, of course, the ``levelsof`` command that eases this but we have not discussed it yet). Anyway, ``by:`` presents the most simple way to do this:

```
bysort lgd_state_name : summarize male_vac

// OR
sort lgd_state_name
by lgd_state_name : summarize male_vac
```

Stata will run the code appearing after the ``:`` for each category of ``lgd_state_name``. Similarly, if we want to summarize ``female_vac`` for each day, we can run:

```
bysort date_year date_month date_day: summarize female_vac

// OR
sort date_year date_month date_day
by date_year date_month date_day: summarize female_vac
```

[Nice read](https://www.stata-journal.com/article.html?article=pr0004)