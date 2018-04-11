---
layout: post
title: Extracting comments from the articles in New York Times
description: "Extracting comments from the articles in New York Times"
headline:
modified:
category: Data Science
tags: [comments-NYT]
imagefeature:
comments: true
share: true
mathjax:
---
I recently contributed a [dataset to Kaggle](https://www.kaggle.com/aashita/nyt-comments) consisting of comments on articles published in the New York Times in March 2018 and Jan-Feb 2017. The blog is intend to put out the code and explain the process so that comments from any time period can be scraped if desired. One can also customize the search of articles to a specific topic - say Iraq war or ObamaCare - along with the timeline by making slight modification to the code below. The data gathered here is stored as two pickled dictionaries - one each for the comments and the articles. These dictionaries can be converted to `csv` files and features can be extracted from them as desired, as explained in the [notebook here](https://www.kaggle.com/aashita/preprocessing-raw-pickled-data-to-csv-file). The collected data comprising of the comments and articles is explored, analyzed and presented with graphs [here](https://www.kaggle.com/aashita/nyt-comments-eda). There are also [word clouds](http://www.aashitak.com/data%20science/Wordclouds) obtained from the most frequent words in the dataset.

### Extracting comments from an article in New York Times

First we import the necessary python modules:


```python
import json
import urllib
from urllib.request import urlopen
from time import sleep
import pickle
```

The following function extracts comments from the New York Times articles given the url of the article.


```python
def nytimes_comments(article):
    '''Given the url of an articles from NYT, returns the list of comments in that article'''
    
    article=article.replace(':','%253A') #convert the : to an HTML entity
    article=article.replace('/','%252F') #convert the / to an HTML entity
    offset=0 # Start off at the very beginning
    total_comments=1 # Initialize the count of comments in the article 
    comment_list=[] # Set up a list to store the comments in the article
    while total_comments>offset:
        url='http://www.nytimes.com/svc/community/V3/requestHandler?callback=NYTD.commentsInstance.drawComments&method=get&cmd=GetCommentsAll&url='+article+'&offset='+str(offset)+'&sort=newest' #store the secret URL
        sleep(1) # NYT do not like you to visit the page too quickly, so we break for a one second 
        file=urlopen(url).read().decode() # Get the comments data and read it into a string
        
        # Clean the file by removing some clutter
        file=file.replace('NYTD.commentsInstance.drawComments(','')
        file=file.replace('      /**/ ','')  at the front end
        file=file[:-2] 
        results=json.loads(file) # Load the file as json
        comment_list=comment_list + results['results']['comments']
        if offset==0: # Print out the number of comments if more than 0, but only the first time through the loop
            total_comments=results['results']['totalCommentsFound'] # Store the total number of comments
            if total_comments > 0:
                print('Found '+str(total_comments)+' comments')

        offset=offset+25 # Increment the counter since 25 comments are scraped each time
        
    return comment_list
```

The above code for scraping the comments is taken from [here](http://nealcaren.web.unc.edu/scraping-comments-from-the-new-york-times/) with some modification to make it work in Python 3. To use the above function, one does not need to be a paid subscriber or use a NYT API-key. All that is needed is the url for the article. NYT does not like us to visit their pages too quickly all at once, so we make the code to take a one second break after every loop and it slowed down the process considerably. In every loop, the function collects 25 comments, so it takes a while to gather lots of comments.

### Extracting lots of comments from the articles in New York Times

To scrap lots of comments from a large number of articles, we can use NYT API to get urls of articles and then use the above function to extract the comments using those urls. The key for using the API can be obtained by registering for NYT API [here](http://developer.nytimes.com/).


```python
API_KEY = '################################' # Please use your API-key here.
NYT_ARTICLE_API_URL = 'https://api.nytimes.com/svc/search/v2/articlesearch.json'
```

The following function uses NYT API to get urls of articles and thereby the comments on those articles. One can easily customize the parameters `params` used in the function to customize the article search to a specific topic. More information on customizing the parameters can be found [here](http://developer.nytimes.com/article_search_v2.json#/README). 


```python
params = {'api-key': API_KEY, 'sort': "oldest"}

def run_rounds(page_lower, page_upper, begin_date, filename):
    '''Collects the comments on the articles of NYT by first scraping the 
    articles using NYT articles search API and then calling on the customized function
    nytimes_comments(url) on each article'''
    
    for page in range(page_lower, page_upper):
        params['page'] = page # Every page has 10 articles
        print("Page: ", page)
        params['begin_date'] = begin_date # We set a begin data
        # Using NYT API to scrap articles
        search_url = NYT_ARTICLE_API_URL + '?' + urllib.parse.urlencode(params)
        file = urlopen(search_url).read() # Get the articles search data and read it into a string
        search = json.loads(file) # Load the articles search data as json
        if search['status'] == 'OK':
            docs = search['response']['docs']
            for i in range(10):
                if docs[i]['document_type'] != 'multimedia': # Ignore multimedia articles
                    article_url = docs[i]['web_url'] # Get the url for the article
                    comments = nytimes_comments(article_url) # Use the article url to get comments 
                    if len(comments)>0: # Check if the article has comments
                        print(article_url)
                        article_id = docs[i]['_id']
                        articles_dict[article_id] = docs[i]
                        comments_dict[article_id] = comments
    save_data(articles_dict, comments_dict, filename)
    print("Total articles stored: ", len(articles_dict))
```

Among all the articles published in NYT in Jan-Feb 2017, roughly 15% of them were open for comments. The code above stores the information only about those articles that have been commented on, but it can be easily modified to store information about all the articles and it can also be modified to store information only about the articles and not the comments. We have also ignored the multimedia articles entirely.

The following function is to store the articles and comments dictionaries as pickled files. The [notebook here](https://www.kaggle.com/aashita/preprocessing-raw-pickled-data-to-csv-file) details the process to load the pickled data and convert it to pandas dataframes. The structure of the dictionaries and the information stored in them is also analyzed in the notebook.


```python
def save_data(articles_dict, comments_dict, filename):
    '''Pickles and saves the articles and comments dictionaries'''
    with open('data/'+ filename + 'article.pkl', 'wb') as f1:
        pickle.dump(articles_dict, f1)
    with open('data/'+ filename + 'comments.pkl', 'wb') as f2:
        pickle.dump(comments_dict, f2)
```

The following is an illustration to run 50 rounds of search (that is to get 500 urls of the articles in NYT) starting April 1st, 2018, extract comments from them and save the data in pickled dictionaries.


```python
comments_dict = {}
articles_dict = {}
run_rounds(page_lower=0, page_upper=50, begin_date = "20180401", filename = 'April2018')
```

The function runs to extract the comments and ends with saving the articles and comments dictionaries using the given filename. The upper limit for `page_upper` is 200 for the NYT API. The API allows a maximum of 1000 searches/rounds per day.

# Acknowledgements
* A part of code used above is inspired from the code written by [Neal Caren](http://nealcaren.web.unc.edu/scraping-comments-from-the-new-york-times/) with some modification.
* NYT API is used to search for url of the articles.
