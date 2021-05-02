---
layout: default
title: browse and edit
nav_order: 2
parent: Stata Commands
grand_parent: Session 1
has_children: false
---

## ``browse``

To see your dataset in the MS-Excel fashion (i..e, as a spreadsheet), run ``browse``. To browse only a selected few variables, you can specify those variables. For example, run ``browse lgd_state_name date total_covaxin``. I often find seeing a dataset in a spreadsheet fashion useful; it provides an intuitive feel for what the data looks like. 

## ``edit``

``edit`` is one of those commands which when you find yourself needing to use, you should step away from the computer and think hard about the decisions that led you to that point in your life. It is similar to ``browse`` in that it opens the dataset as a spreadsheet but you can now edit the data by typing in the cells. Do not do this, please! If you need to replace certain values in certain variables, you should do them using the if statement in the ``replace`` command so that your changes are programmable and reproducible. (we cover ``replace`` in a subsequent section)