---
layout: default
title: Local macros
nav_order: 3
parent: Session 2
has_children: false
---

The essential function served by local macros is similar to global macros: to store values. However, global macros stay in the memory long after their execution whereas local macros are dropped after the code is executed. In most cases, we do not need the value beyond a particular chunk of code and so, it is advisable to use local macros. Since we need file paths throughout the do-file and we may run part of the code here and there, file paths should be saved in global macros. To remain brief, we call them globals and locals, i.e., no need to append "macros" at the end.

Another difference arises in the coding. To create a local macro, we use the ``local`` command, to reference it, we use `` ` ' ``.