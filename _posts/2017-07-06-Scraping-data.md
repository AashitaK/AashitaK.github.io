---
layout: post
title: Scrapping data from the internet 
description: "Scraping data from the internet using Python"
headline:
modified: 
category: articles
tags: [data-scraping]
imagefeature: 
comments: true
share: true
mathjax:
---
The first step for a data science project is to obtain the data to work with. 
In this age of [Kaggle](https://www.kaggle.com/) and the abundance of datasets freely available in read-to-use format to learn and practise 
data science tools, the various tools available in python for data-scraping from the internet can often be missed out. In real life data science projects, a data scientist need not be given data in the most desirable format and should know how to collect the data by herself/himself.

[//]: # (Knowing how to gather data available on the internet gives one more flexibity and independence to choose a project of one's own liking.) 
I find the course [*Using Python to Access Web Data*](https://www.coursera.org/learn/python-network-data) by University of Michigan on Coursera very informative. This blog is an attempt to give a brief overview of what I learnt from this course by [Prof. Charles Severance](http://www.dr-chuck.com/).

The data on internet comes in many formats, most commonly JSON, XML or just plain old HTML. Python library `urllib` lets one access data directly from the URL of a website. Based on the format of the data retrieved, there are Python libraries, like `json, xml.etree.ElementTree, BeautifulSoup, pickle, socket`, to extract useful information from that data.

To be continued...
