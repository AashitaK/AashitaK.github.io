---
layout: page
permalink: /about/index.html
title: Aashita Kesarwani
tags: [Aashita, Kesarwani, akesarwa, aashitak, aaashitak, IIT, Roorkee, Gondia, Tulane, data scientist, machine learning, PhD]
imagefeature: 
chart: true
mathjax: true 
---
I am a Math PhD graduate with a passion for data and machine learning. I am especially interested in two particular areas - data visualizations and natural language processing.

Open source contributions related to data science: 
- [Bubbly](https://pypi.org/project/bubbly/) (Author and Maintainer)  
An easy-to-use python package for plotting interactive and animated bubble charts using plotly. The animated bubble charts can accommodate upto seven variables in total viz. X-axis, Y-axis, Z-axis, time, dots, their size and their color in a compact and captivating way with plenty of customization and can be used with plotly [as demonstrated in the notebook here](https://www.kaggle.com/aashita/guide-to-animated-bubble-charts-using-plotly).

![Bubble plot](/images/bubblechart.gif)

- [nytcomments](https://pypi.org/project/nytcomments/) (Author and Maintainer)   
A Python package that includes three main functions to perform three distinct tasks involving the retrieval of comments' and articles' from New York Times as ready-to-use dataset for data science/machine learning projects:
    1. The main function **get_dataset** returns two dataframes - one each for the articles and the respective comments. The retrieval can be customized based on a number of parameters such as a specific timeline for the articles, search keywords, filter queries, etc.   
    2. The function **get_articles** is an API wrapper for NYT article search API, that returns the cleaned up and preprocessed data for articles as a ready-to-use pandas dataframe (or csv files) and the retrieval can be customized with the same options as above.
    3. The function **get_comments** retrieves the comments on NYT article(s) given their URLs. It can be used as a substitute for the comments by URL option in the NYT Community API that is now deprecated and has an [unresolved issue](https://github.com/NYTimes/public_api_specs/issues/29). This function does not use NYT API for the retrieval unlike the above two.
The package is accompanied with an [illustrative tutorial](https://github.com/AashitaK/nyt-comments/blob/master/Tutorial.ipynb) for its use containing detailed information regarding the functions and their parameters. 

- A [dataset](https://www.kaggle.com/aashita/nyt-comments) contributed to Kaggle, that was among the 20 featured datasets, comprised of over 1.2 million comments with 34 variables and over 9,000 articles with 16 variables along with the ideas for data science projects.
 
Project concerning comments posted on New York Times articles:
- [Exploratory data analysis](https://www.kaggle.com/aashita/exploratory-data-analysis-of-comments-on-nyt) of the features contained in the comments' and articles' dataset with statistical graphs. 
- [Bag of words models](https://www.kaggle.com/aashita/predicting-nyt-s-pick) to predict the probability that a certain comment will be selected as a NYT's pick. 
  1. Logistic Regression model coupled with Latent Semantic Analysis (LSA) on Tf-Idf vectors of words and character n-grams of comments' text.
  2. NB-Logistic Regression model inspired from the paper [Baselines and Bigrams: Simple, Good Sentiment and Topic Classiﬁcation](https://nlp.stanford.edu/pubs/sidaw12_simple_sentiment.pdf) by Sida Wang and Chris Manning.
  
Cool projects related to NYT dataset:
- An automated twitter bot [@OnAffairs](https://twitter.com/OnAffairs) trained to comment on current affairs using the Markov chain model on comments from NYT articles. [[Code]](https://github.com/AashitaK/CurrentOnAffairs)
- [Word clouds](http://www.aashitak.com/data%20science/Wordclouds) of various shapes for the visualization of different  textual features from the NYT articles' and comments' dataset.

Some of my past projects can be found at the following links:
- [Titanic survival prediction](https://www.kaggle.com/aashita/xgboost-model-with-minimalistic-features) (Top 3% score in Kaggle competition)
- Feature Engineering for [2018 NCAA Division I Men’s Basketball Championships](https://www.kaggle.com/aashita/feature-engineering-for-march-madness) predictions
- [The effect of recession on housing prices in university towns](http://www.aashitak.com/projects/Testing-Hypothesis)
- [Plotting record temperatures for New Orleans](http://www.aashitak.com/projects/Plotting-Temperatures-NOLA)
- [Extraction of dates from medical records](https://github.com/AashitaK/aashitak.github.io/blob/master/_posts/Extracting%20dates%20from%20medical%20records.ipynb)

My PhD thesis titled *Theory of the generalized modified Bessel function \\(K_{z,w}(x)\\) and \\(2\\)-adic valuations of integer sequences* is linked [here](https://digitallibrary.tulane.edu/islandora/object/tulane%253A77514).

[//]: #(![Here](/images/Aashita_resume.pdf) is a link to my resume [Aashita Kesarwani](/images/Aashita_resume.jpg){:width="1080px"})

Please feel free to contact me at [contact@aashitak.com](mailto:contact@aashitak.com) or connect with me in other platforms (Github/LinkedIn/Kaggle) using the icons at the bottom bar of the website.
