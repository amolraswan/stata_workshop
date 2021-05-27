---
layout: default
title: Short assignment
nav_order: 7
parent: Session 3
has_children: false
---

Use the folder structure from [here](https://amolraswan.github.io/stata_workshop/session2/1_project_folder/). Write your answers in a do-file and **submit the whole folder** (rename it suitably: *name_session3assignment*). Do not delete the empty sub-folders. At the top of the do-file, mention your name, date, and purpose of the do-file. Follow the do-file system from [here](https://amolraswan.github.io/stata_workshop/session3/1_do_file_system/).

For each question below, first write a comment signalling the question number, then a very brief description about what you need to do/are going to do, then the code, and then write the final answer (if the question asks for it, like number of observations). 

We continue with the vaccination data available [here](https://drive.google.com/file/d/1Sb86BVYAgiyqpg7QsBdNvfWfG9Y63UGy/view?usp=sharing). Remember to save it in the ``01_raw_data`` folder!

1. Keep the following variables: ``lgd_state_name``, ``lgd_district_name``, ``date_day``, ``date_month``, ``total_covaxin``, and ``total_covishield``.

2. The data is currently at a district-day level. We want to transform it to the state-day level. Follow these steps:

	a. Add up the values of ``total_covaxin`` and ``total_covishield`` at the state-day level. That is, for each day, we want to add the respective vaccination variables to get at the state-level figure. Use the ``sort`` + ``by`` or the ``bysort`` command and then the ``total`` function of the ``egenerate`` command.

	b. The resultant data will have duplicates in the state and date variables. Drop duplicates using the ``duplicates drop`` command. 

	c. Save the dataset (name it appropriately) in the ``final_data`` folder.

3. Start over from the raw dataset. Repeat step 2 but now expand the list of variables to ``total_covaxin``, ``total_covishield``, ``male_vac``, ``female_vac``, and ``trans_vac``. What you should try doing here is to use a for-loop in step 2.a so that you don't have to write the ``bysort`` and ``egen`` chunk repeatedly for each variable. Save the resultant dataset (name it differently from what you did in 2.c) in the ``final_data`` folder. 

4. Lets use the dataset from step 2.c. It contains the number of covaxin and covishield shots administered on each day in different states. A metric we would be interested in looking at is the cumulative number of vaccinations. On a given date, such a variable will equal the sum of vaccinations administered until then. The ``sum`` function of the ``generate`` command does this. Type ``help sum()`` to see its help file. Create a variable called ``total_covaxin_cumm`` that is a cumulative sum of ``total_covaxin`` over time for each state.

	a. Sort the dataset on ``lgd_state_name``, ``date_day``, and ``date_month``. After sorting, browse the data to ensure it looks alright.

	b. Use the ``by`` alongwith ``generate`` (and its ``sum`` function) to create the variable.

	c. Refer to this [related problem](https://www.statalist.org/forums/forum/general-stata-discussion/general/1349906-cumulative-sum-by-group) for hints on how to do this using ``bysort``. Adapt it to our context and create ``total_covaxin_cumm2`` using ``bysort``.

