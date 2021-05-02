---
layout: default
title: Short Intro to Stata
nav_order: 1
parent: Session 1
has_children: false
---

Stata is a statistical software. As such, its job is to provide user-friendly tools to for data manipulation and analysis. It is not a programming language (though Stata has its own programming lanuage called Mata which we will not cover in this workshop). Stata takes a dataset as the starting point and makes it easier for the user to clean and transform this data, and then run analysis on the final data. This is unlike programming languages such as Python and R which can have many different types of objects stored in the memory and allow the user to easily switch between them. Mind you, Stata also allows the user to work on different types of objects at the same time, but because its focus is on a dataset, working with multiple objects is as painful in Stata as it is seamless in Python or R. What are these objects? These can be a matrix, a variable that equals 5, a vector, a list, etc. 

Stata is best understood as an evolved form of MS-Excel: a software that works with a dataset (which looks like a spreadsheet when opened in Stata's data browser) but gives the user programming capabilities to have:

- reproducibility
- programmability 

You get the above two benefits when you save your commands in a script, which is called a do file in Stata. Reproducibility means that with your original dataset and do file, anyone can arrive at your final dataset. Programmability means that if you want to re-run your cleaning or analysis commands again, you can simply re-run the commands in the do-file. These two reasons give Stata an unassailable edge over MS-Excel; never use MS-Excel for data cleaning and analysis (some very preliminary data work or results preparation is, of course, permissible).

Though R is much more flexible and versatile (and is free!) than Stata, it is also more difficult to learn as a beginner. Stata's documentation for its commands is superb. Add on to these two benefits the fact that most researchers use Stata for most of their tasks, you can see why it makes sense at an individual level to start with Stata and later transition to R. If we could somehow remove network effects from the equation, then it would be better for the whole world to switch to R; sadly, we can't do that. 

Stata recently released Stata 17. The number at the end signifies the version. You *never*need the latest version. Anything from Stata 13 and above is good enough. 

A short, slightly fast [introduction](https://www.youtube.com/watch?v=2Lde75owQlU) to Stata's user interface. 