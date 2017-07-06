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
data science tools, one may miss out the various tools available in python for data-scraping from the internet. In certain data science projects, data may not be readily available in the desirable format, but need to be mined from the internet. For this purpose, I find the course [*Using Python to Access Web Data*](https://www.coursera.org/learn/python-network-data) by University of Michigan on Coursera taught by [Prof. Charles Severance](http://www.dr-chuck.com/) very informative. This blog is an attempt to give a brief overview of the tools taught in this course in a way that can be grasped by a beginner in data science.

[//]: # (Knowing how to gather data available on the internet gives one more flexibity and independence to choose a project of one's own liking.) 

The data on internet comes in many formats, most commonly JSON, XML and ofcourse plain old HTML. Python library `urllib` lets one access data directly from the URL of a website. Based on the format of the data retrieved, there are Python libraries, like `json, xml.etree.ElementTree, BeautifulSoup, pickle`, to extract useful information from that data.

### BeautifulSoup
[BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/) is one of the widely used Python library for web-scraping i.e. searching through websites on the internet to extract only the relevant data. It is used to parse data from the HTML or XML files. It takes a file and makes a soup out of its content so that the target information can be extracted easily and efficiently from an enormous amount of irrelevant data. 

### Json
Json library in Python is specially designed to work with JSON files. 
To be continued...
