---
layout: default
title: Short assignment
nav_order: 4
parent: Session 1
has_children: false
---

Submit your answers in a do-file. At the top of the do-file, mention your name, date, and purpose of the do-file. For each question below, first write a comment signalling the question number, then a very brief description about what you need to do/are going to do, then the code, and then write the final answer (if the question asks for it, like number of observations).

1. Researchers often standardize variables to put them all on a standard scale. These are called [z-scores](https://en.wikipedia.org/wiki/Standard_score) (read it if you don't know about z-scores). This is especially important when you want to create an index of different variables. For example, suppose you want to rank Indian districts based on an index composed of number of vaccinations and number of ventilators available. You obviously can't simply add the two variables; they are in very different measurement units. So, instead, you can standardize them which ensures that they are in terms of their standard deviation units, and then take a weighted sum. 

	1. Standardize the following variables: ``total_covishield``, ``total_covaxin``, and ``female_vac``. For standardization, use the mean and standard deviation derived from the whole sample. Do not overwrite the variables; instead, create new variables called: ``total_covishield_stan1``, ``total_covaxin_stan1``, ``female_vac_stan1``. Remember: standardized variable = (variable - mean)/standard deviation.

	2. The mean and standard deviation used in standardization above were derived from the whole sample. Now do it a bit differently. For each month, compute the mean and standard deviation of the variable, and use these to standardize the observations for that month. For example, for variable ``total_covaxin`` and month January, you'd compute the mean and standard deviation of ``total_covaxin`` for the month of January; and then use these to generate the standardized values of total_covaxin for January observations. Call the new variables ``total_covishield_stan2``, ``total_covaxin_stan2``, ``female_vac_stan2``.

2. Consider the Anantnag district in Jammu and Kashmir. On what date did it have the highest number of covishield vaccinations administered? Of covaxin vaccinations administered? (Hint: use the commands ``summarize`` and ``tabulate``)


3. We previously used the ``!`` operator with ``missing()`` to define ``!missing()`` as not missing. Similarly, ``!(lgd_state_name == "gujarat")`` means non-Gujarat observations. ``!`` "negates" the expression inside the parentheses. Another example: ``!(total_covaxin > 500)`` is equivalent to ``total_covaxin <= 500``. To negate ``inlist()`` and ``inrange()``, we write ``!inlist()`` and ``!inrange()``. The negation operator is the same as the one in set theory in mathematics and if I remember one thing from it, it was that it can often be confusing. So, be careful!

	1. Count the number of observations that belong to states other than Uttarakhand and Tripura. 

4. Consider Birbhum district in West Bengal. On how many days did this district have:

	1. More covaxin shots than covishield shots?
	2. More males getting vaccinated than females?
	3. More males getting covaxin shots than females getting covishield shots? 
