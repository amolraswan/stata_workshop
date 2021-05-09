---
layout: default
title: Project folder
nav_order: 1
parent: Session 2
has_children: false
---

The following advice works mostly well for small to medium sized projects. If you have a large project with data coming in from multiple sources or multiple people working on multiple kinds of analysis, you may have to think more deeply about folder organization. Nevertheless, what follows is simply a suggested outline and you should feel free to play around with it.

We want to have a separate folder for each project and within that main folder, different sub-folders for unrelated items. Let's say your project is "Session 2". One particular way of managing your directory structure (i.e., project structure) could be to have the following sub-folders in the "Session 2" folder:

- 01_data
	- 01_raw_data
	- 02_processed_data
	- 03_final_data
- 02_code
- 03_result
	- 01_tables
	- 02_graphs

All folder names here start with a number which helps us control the order in which they appear when we open "Session 2". We will come back to 02_code at the session's end to discuss what all do-files we need to have. Now is slightly premature to kick off that discussion but we will hopefully be able to have it after learning about global macros. The 01_data folder has three sub-folders, each for raw data, processed data, and final data. On a simple enough project, you might not have any processed data, i.e., data that's somewhere between raw and final. Raw data means your original datasets while final data means the cleaned datasets that you will run your analysis on.  

These are simply suggestions. For example, instead of having raw and final data folders within 01_data, you could straightaway have two main folders: 01_raw_data and 02_final_data. Could do the same for tables and graphs folders; i.e., instead of keeping them in 03_result, bring them out in the main directory. Implementing these two changes, our Session 2 folder would look like:

- 01_raw_data
- 02_final_data
- 03_code
- 04_tables
- 05_graphs

There are numerous possible customizations here. For now, we will stick to the original version. For clarity, I have uploaded an empty sample directory [here](https://drive.google.com/file/d/1CCe124cdJ70KaEI5NTlr-9x7EzqK63Pf/view?usp=sharing). We will use its folder structure for illustration purpose today.