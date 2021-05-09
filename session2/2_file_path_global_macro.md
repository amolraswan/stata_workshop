---
layout: default
title: File paths and global macro
nav_order: 2
parent: Session 2
has_children: false
---

Irrespective of whether you use the folder structure that we discussed, your do-file(s) will have you using file paths (i.e., address of the file on your computer) at multiple points: loading the dataset, saving the cleaned dataset, exporting a graph, etc. 

I have kept the session_2 folder on my computer's desktop. So, its file path looks something like: ``C:/Users/amolr/Desktop/session_2``. I am using the earlier proposed folder structure, so my raw data's file path is ``C:/Users/amolr/Desktop/session_2/01_data/01_raw_data``, graphs' path is ``C:/Users/amolr/Desktop/session_2/03_result/02_graphs``, etc. Since there are likely to be multiple graphs exported on a single project, you can expect the file path to appear numerous times in the do-file. 

Now suppose I send you my session_2 folder for replication and further work. To get started on things, you will have to replace the folder address (of session_2) accordingly at multiple points. Even more troublesome would be the situation where we both work together out of Dropbox and we'd have to change part of the file path each time we run the do-file. 

To solve this issue, we need a way to "store" ``C:/Users/amolr/Desktop/session_2`` in a "variable" and then reference this variable in subsequent file paths. Note the double quotes on "variable": creating a variable in Stata means creating a variable in the dataset that we are working on but that's not what we want. We want to create an object that equals the string ``C:/Users/amolr/Desktop/session_2``. This is quite straightforward in programming languages such as Python and R; for example, you can simply set ``x = C:/Users/amolr/Desktop/session_2`` in Python. In Stata, we can do this by way of **macros**. Note that these macros are entirely different from the macros in MS-Excel. Instead they are similar to the ``x`` we created in Python above. 

Stata has two types of macros: ``global macro`` and ``local macro``. We will learn about ``global macro`` now. Let me first present an example code:

```
// setting up globals
	global projdir "C:/Users/amolr/Desktop/session_2"
	global raw_data "${projdir}/01_data/01_raw_data"
	global final_data "${projdir}/01_data/03_final_data"

// importing the vaccination dataset as of 2021.04.18
	use "${raw_data}/covid_vaccination_2021_04_18.dta", clear
```

To create a global macro, we first specify ``global`` to let Stata know that we want to create a global macro. Next comes the name ``projdir`` and then its value ``"C:/Users/amolr/Desktop/session_2"``. This is equivalent to writing ``projdir = "C:/Users/amolr/Desktop/session_2"`` in Python. Why do I keep bringing up Python? For no reason other than to make you comfortable with the idea that macros are simply objects that store a single or multiple values (for now, we are storing single values). Now, to reference the ``projdir`` macro at other places, I write ``${projdir}``. The curly brackets are not necessary in this situation but they sometimes become necessary, so I recommend always using them. Why do we need to specify the global as ``${projdir}`` and not simply ``projdir`` when we were trying to create the global raw_data? Suppose we had written ``global raw_data "projdir/01_data/01_raw_data"``. Stata would not know if projdir is part of the string or refers to the global. It will assume the former. So, we use ``${..}`` format. We similarly referenced the ``raw_data`` global in the file path for ``use`` command. 

Now, if I were to share the session_2 folder with you, you will only have to change the value of the ``projdir`` global and everything else will adjust automatically!

**Important:** In general, you should not use global macros for other than defining file paths. We will discuss why so in the next page on local macros. Just letting you know that the first preference should be for local macros (for tasks other than defining file paths).

Truth be told, instead of defining global macros, we could have got around the posed issue by changing the directory that Stata is working in. Execute ``pwd`` to get the working directory. For me, ``pwd`` returns ``C:/Users/asr2776/Documents``. This is the base path that Stata considers; If we didn't specify full file paths and were to instead write ``use "01_data/01_raw_data/covid_vaccination_2021_04_18.dta", clear``, Stata would look for the ``01_data`` folder in ``C:/Users/asr2776/Documents``. So, we could change the directory using the ``cd`` command: ``cd "C:/Users/amolr/Desktop/session_2"``. ``use "01_data/01_raw_data/covid_vaccination_2021_04_18.dta", clear`` now works!
