---
layout: default
title: "Session 1"
nav_order: 2
has_children: true
has_toc: true
---

# Session 1

We will use covid19 vaccination data for India as the example dataset for today's session. It has been compiled, cleaned, and made publicly available by the [Development Data Lab](http://www.devdatalab.org/covid). I cannot emphasize enough the awesome work being done by this team, go check out the datasets they have painstakingly cleaned and linked to each other! Anyway, the dataset we will focus on is called covid_vaccination.dta [here](https://www.dropbox.com/sh/y949ncp39towulf/AADbSeZWSG1xjPHXNMTyhmoba/covid?dl=0&subfolder_nav_tracking=1).

I have added a few variables to this dataset and saved a copy on [my drive](https://drive.google.com/file/d/1Sb86BVYAgiyqpg7QsBdNvfWfG9Y63UGy/view?usp=sharing). We will use this version.  

Before delving into any kind of cleaning or analysis, it is important to understand the dataset's structure. I'm going to give you a spoiler for now but you will learn commands today that can help you do the same. The dataset has vaccination estimates at the district-date level. What does district-date level? Each row represents a unique combination of a district and a day. So, say, for Karnal (Haryana), we will have multiple observations, all pertaining to different dates. Another way to put it: the data contains daily vaccination estimates at the district level.

