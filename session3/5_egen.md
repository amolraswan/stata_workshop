---
layout: default
title: Egen
nav_order: 5
parent: Session 3
has_children: false
---

Egen stands for extensions to generate. It is used for creating new variables, the difference from ``generate`` being that ``egen`` has a large library of functions to choose from. 

For instance, suppose you want to create ``total_vac`` as a sum of ``male_vac``, ``female_vac``, and ``trans_vac``. We can do this using ``gen total_vac = male_vac + female_vac + trans_vac`` but can also use the ``rowtotal`` function of ``egen``: ``egen total_vac = rowtotal(male_vac female_vac trans_vac)``. ``rowtotal`` has a little pathology related to missing values, though; it treats missing values as zeroes, which often is not the desired outcome. So, be careful about what you want!

You can check out the list of functions in ``egen`` in its help file (``help egen``). Though its introduction might seem a bit disparate, we are covering it today because it is often used with ``by`` (or ``bysort``) which is today's central topic.