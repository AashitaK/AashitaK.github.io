---
layout: page
permalink: /about/index.html
title: Aashita Kesarwani
tags: [Aashita, Kesarwani, akesarwa, aashitak, aaashitak, IIT, Roorkee, Gondia, Tulane, data scientist, machine learning, PhD]
imagefeature: 
chart: true
mathjax: true 
---
I am a recent math PhD graduate and a machine learning enthusiast. Below are some of the links detailing my current project concerning comments posted on New York Times articles.
- A [dataset](https://www.kaggle.com/aashita/nyt-comments) comprising of over ***2 million comments with 34 features*** as well as ***16 features*** concerning over ***8750 NYT articles*** spanning Jan-May 2017 and Jan-April 2018 to Kaggle along with the ideas for data science projects. The dataset is currently at the [top among the 20 featured datasets](https://www.kaggle.com/aashita/nyt-comments) on Kaggle.
- A [Python package](https://github.com/AashitaK/nyt-comments) that includes three main functions to perform three distinct tasks involving the retrieval of comments' and articles' from New York Times as ready-to-use dataset for data science/machine learning projects:

1. The main function ``get_dataset`` returns two dataframes - one each for the articles and the comments on them. The retrieval can be customized based on a number of optional parameters such as a specific timeline for the articles, search keywords, filter queries based on a number of options such as the week of the day, the word count of the articles, source, etc., maximum limit on the number of comments or articles or both, sorting the articles chronologically based on either the newest or oldest articles, option to suppress or activate the output log for the process, option to save the data as two `csv` files, etc. The function returns only the articles that were open to comments along with the comments on them.   

2. The function ``get_articles`` can be used as an API wrapper for NYT article search API. It returns the cleaned up and preprocessed data for articles as a ready-to-use pandas dataframe (with an option to store it in ``csv`` files) and the retrieval can be customized with the same options as above.

3. The function ``get_comments`` retrieves the comments on NYT article(s) given their urls. It can be used as a substitute for the comments by url option in the NYT Community API that is now deprecated and only return comments that were picked as editor's selection on account of an [unresolved issue](https://github.com/NYTimes/public_api_specs/issues/29). This function does not use NYT API for the retrieval unlike the above two.

- The package is accompanied with an [illustrative tutorial](https://github.com/AashitaK/nyt-comments/blob/master/Tutorial.ipynb) for its use containing detailed information regarding the functions and their parameters.
- [Exploratory data analysis](https://www.kaggle.com/aashita/nyt-comments-eda) of the features contained in the comments' and articles' dataset with statistical graphs. 

- [Logistic regression model](https://www.kaggle.com/aashita/starter-kernel-for-predicting-nyt-s-pick/log) built with features generated using Tfidf vectorizer on words and character n-grams of comments' text to predict the probability that a certain comment will be selected as NYT's pick. 
- [Word clouds](http://www.aashitak.com/data%20science/Wordclouds) from the dataset for fun. 

[Here](/images/Aashita_resume.pdf) is a link to my resume and some of my past projects can be found at the following links:

[//]: #(![Aashita Kesarwani](/images/Aashita_resume.jpg){:width="1080px"})


- [Titanic survival prediction](https://www.kaggle.com/aashita/xgboost-model-with-minimalistic-features) (Top 3% score in Kaggle competition)
- Feature Engineering for [2018 NCAA Division I Men’s Basketball Championships](https://www.kaggle.com/aashita/feature-engineering-for-march-madness) predictions
- [The effect of recession on housing prices in university towns](http://www.aashitak.com/projects/Testing-Hypothesis)
- [Plotting record temperatures for New Orleans](http://www.aashitak.com/projects/Plotting-Temperatures-NOLA)
- [Extraction of dates from medical records](https://github.com/AashitaK/aashitak.github.io/blob/master/_posts/Extracting%20dates%20from%20medical%20records.ipynb)

[Below](https://www.linkedin.com/in/aashita-kesarwani) is my LinkedIn profile:
<pre>
<script type="text/javascript" src="https://platform.linkedin.com/badges/js/profile.js" async defer></script>
<!--div class="LI-profile-badge"  data-version="v1" data-size="large" data-locale="en_US" data-type="horizontal" data-theme="dark" data-vanity="aashita-kesarwani"><a class="LI-simple-link" href='https://www.linkedin.com/in/aashita-kesarwani?trk=profile-badge'>Aashita Kesarwani</a></div-->
<!--div class="LI-profile-badge"  data-version="v1" data-size="medium" data-locale="en_US" data-type="vertical" data-theme="dark" data-vanity="aashita-kesarwani"><a class="LI-simple-link" href='https://www.linkedin.com/in/aashita-kesarwani?trk=profile-badge'>Aashita Kesarwani</a></div-->
<div class="LI-profile-badge"  data-version="v1" data-size="large" data-locale="en_US" data-type="vertical" data-theme="dark" data-vanity="aashita-kesarwani"><a class="LI-simple-link" href='https://www.linkedin.com/in/aashita-kesarwani?trk=profile-badge'>Aashita Kesarwani</a></div>
</pre>

[//]: #([Here](https://github.com/AashitaK) is the link to my GitHub account containing some of the simple projects I completed recently as I am learning tools for data science and machine learning.)

Please feel free to contact me at [contact@aashitak.com](mailto:contact@aashitak.com) or connect with me in other platforms using the icons at the bottom bar of the website.
