---
layout: default
title: Short assignment
nav_order: 4
parent: Session 2
has_children: false
---

Use the folder structure from [here](https://amolraswan.github.io/stata_workshop/session2/1_project_folder/). Write your answers in a do-file and **submit the whole folder** (rename it suitably: *name_session2assignment*). Do not delete the empty sub-folders. At the top of the do-file, mention your name, date, and purpose of the do-file. For each question below, first write a comment signalling the question number, then a very brief description about what you need to do/are going to do, then the code, and then write the final answer (if the question asks for it, like number of observations). This assignment is aimed at helping you become comfortable with using macros. So, **use global macros to define your file paths**.

We continue with the vaccination data available [here](https://drive.google.com/file/d/1Sb86BVYAgiyqpg7QsBdNvfWfG9Y63UGy/view?usp=sharing). Remember to save it in the ``01_raw_data`` folder!

1. Calculate the sum of first 50 whole numbers (0 to 49) using a ``forvalues`` loop. **Hint**: we can add to the value of an existing local macro. For example, we can declare a local x that equals 5: ``local x = 5``. And then increment x's value by 7: ``local x = `x' + 7``. (Note that the ``=`` sign is superfluous in both the first and second steps)

2. We learnt the flexibility offered by the ``rename`` command in [session 1](https://amolraswan.github.io/stata_workshop/session1/3_statacommands/rename/). In the second to last example on that page, we learnt how to remove the suffix ``date_`` from the variables that have it. There were 3 such variables: ``date_day``, ``date_month``, and ``date_year``. Let us try doing this using a ``foreach`` loop now. Follow these steps:

	1. First define a local that contains three elements: ``"day month year"``.

	2. Imagine doing it for one variable, say, ``date_day``. How would we write it? Something like: ``rename date_day day``. 

	3. Now that we have to write a general loop statement, our ``rename`` command would go inside the loop statement and look something like: ``rename date_`x' `x' ``. Ensure that you understand how this works. `` `x' `` here will call upon the relevant loop element and place it at the relevant spots. So, when ``x == "month"``, the command would be executed as: ``rename date_month month``. 

	4. Complete the loop statement, i.e., write the actual ``foreach`` part. Remember, since we wrote ``x`` in step 3, your command should start with ``foreach x of ...``. Feel free to write something else instead of ``x``.

3. We have three variables called ``male_vac``, ``female_vac``, and ``trans_vac``. Using a ``foreach`` loop, rename them as ``total_vac_male``, ``total_vac_female``, and ``total_vac_trans``, respectively. **Hint**: Similar to Question 2.1 above, your initial local should contain these elements: ``male female trans`` and for step 3, your rename command should look like: ``rename `x'_vac ...``. You need to fill the ``...``!

4. Display the mean number of covishield vaccinations on each day of March. **Hint**: There are two parts:

	1. First write a ``forvalues`` loop to summarize the ``total_covishield`` variable for each day of March and store the ``r(mean)`` value in a local. Remember that your local's name should change by the day, so perhaps something like: ``local mean_on_`x'_march `r(mean)' `` where ``x`` comes from the ``forvalues`` statement.

	2. Write another ``forvalues`` loop that goes through the day-wise locals you defined in step 1 and then displays the mean value on each day in a "nice" way. Make it "nice" by writing a descriptive ``display`` command, so something like: ``display "Mean covishield vaccinations on `y' March were: ..."``. You need to fill in the ``...`` with the suitable local name. Note that here, I am using ``y`` in the ``forvalues`` statement.

	3. Note: Both ``forvalues`` statements should go from 1 to 31 since you want to loop over the days in March.

5. Save the edited dataset in the ``02_processed_data`` folder. (add "\_edited" at the end of its name)
