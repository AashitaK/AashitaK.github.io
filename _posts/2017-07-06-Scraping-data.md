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
Json library in Python is specially designed to work with JSON files. [JSON](http://www.json.org/)(JavaScript Object Notation) is one of the two data-interchange language, the other being XML. There are two type of data structures common to almost all modern programming languages - the collection of key/value pairs, for e.g. dictionaries in Python, and the ordered list of values, for e.g. lists in Python. The simple idea behind the conception of JSON by [Douglas Crockford](https://en.wikipedia.org/wiki/Douglas_Crockford) was that the data format used to exchange data between programming languages be based on these universal data structures. They are called object and array respectively in JSON inheriting the terminology and syntax from JavaScript.

### Xml.etree.ElementTree
Xml.etree.ElementTree library in Python is specially designed to work with XML files. XML(Extensible Markup Language) is a markup language, like HTML, designed to store and exchange data in a format that is both human-readable and machine-readable. Like HTML, it has tags and a tree-like structure. This library works similar to BeautifulSoup above?

To be continued...
