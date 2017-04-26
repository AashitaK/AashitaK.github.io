---
layout: post
title: Plotting record temperatures for New Orleans over the period 2005-2015
description: "Plotting record temperatures for New Orleans over the period 2005-2015 using pandas and matplotlib."
modified: 2017-04-21
category: articles
tags: [plotting]
imagefeature: coverNOLA.jpg
comments: true
share: true
---

One of the things I love about New Orleans is its warm and optimistic weather. The bright and sunny days happen all year round, at times more often than I wish for. I let ```pandas``` and `matplotlib` tell the rest of the story and give a clear picture of the temperature trends in New Orleans over 2005-2015.

<figure>
  <img src = "" alt = "Temperature graph">
  <figcaption>
</figure>


In the notebook, the highest and lowest temperatures for New Orleans is extracted for each day of the year over the 
period 2005-2014 using `pandas`. 
These highs and lows are plotted as line graphs using `matplotlib` and 
then record breaking temperatures for the year 2015 are scattered in the same graph. 
Both the Celsius and Fahrenheit scales are included as the left and right y-axis respectively; 
the month labels are centrally placed between the ticks denoting the start and end of each month in the x-axis. 
The verbal description in terms of legends, labels and title is minimalist, 
and every aspect of the graph, including the color palette, is thoughtfully chosen to convey the information visually. 
The effort is to make the graph look neat, accurate, informative and visually appealing. 

The idea and guidance for this exercise was taken from the online course [Applied Plotting, Charting & Data Representation in Python](https://www.coursera.org/learn/python-plotting) by University of Michigan on [coursera](https://www.coursera.org/). 
[The National Centers for Environmental Information (NCEI) Daily Global Historical Climatology Network (GHCN-Daily)](https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/readme.txt) contains daily climate records from 12 stations near New Orleans. 
The temperatures over the period Jan 01, 2005 to Dec 31, 2015 in the ready-to-use `csv` format can be found in my github repository [here](https://github.com/AashitaK/Plotting-Record-Temperatures). 


