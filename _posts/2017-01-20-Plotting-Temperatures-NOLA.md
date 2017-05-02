---
layout: post
title: Plotting record temperatures for New Orleans 
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
  <img src = "{{ site.url }}/images/NOLATemp.png" alt = "Temperature graph">
  <figcaption>Temperature Trends in NOLA </figcaption>
</figure>

In the graph, the record highs and lows in the temperature over the period 2005-2014 are plotted as line graphs and then record breaking temperatures for the year 2015 are scattered as red and blue dots in the same graph. 
The idea and guidance for this exercise is taken from the online course [Applied Plotting, Charting & Data Representation in Python](https://www.coursera.org/learn/python-plotting) by University of Michigan on [coursera](https://www.coursera.org/). 

[The National Centers for Environmental Information (NCEI) Daily Global Historical Climatology Network (GHCN-Daily)](https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/readme.txt) contains daily climate records from 12 stations near New Orleans. 

The temperatures over the period Jan 01, 2005 to Dec 31, 2015 in the ready-to-use `csv` format can be found in my github repository [here](https://github.com/AashitaK/Plotting-Record-Temperatures). The `pandas` library is used to extract the temperature in Dataframes.

Reading the data from the csv file into pandas dataframe
```python
import pandas as pd
import numpy as np
filename = "data_temperatures_nola.csv"
df = pd.read_csv(filename) 
```
Temperatures are given at tenths of degrees celsius. The following is preparing the dataframe to extract the desired data
```python
df.loc[:,'Data_Value'] *= 0.1 # Dividing all temperature entries by 10 to convert them to degree celsius
df['Date'] = pd.to_datetime(df['Date']) # Changing the dtype of the date to pandas datetime 
```
Setting up the sorted multi-index consisting of month and days so as to help grouping rows later for each day of the year.
```python
df['Day'] = pd.DatetimeIndex(df['Date']).day 
df['Month'] = pd.DatetimeIndex(df['Date']).month 
df = df.set_index(['Month','Day']) 
df.sort_index(inplace = True)
```
Discarding all the entries for 29th Feb of any year; only 365 days of the year are considered
```python
selected_df = df.loc[2,29] 
df = df[~df.index.isin(selected_df.index)]
```























