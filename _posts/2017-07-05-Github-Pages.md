---
layout: post
title: Setting up website using Github Pages 
description: "Setting up website using Github Pages"
headline:
modified: 
category: articles
tags: [webpage]
imagefeature: 
comments: true
share: true
mathjax:
---


The [GitHub Pages](https://pages.github.com/) lets you make your own website. It is very well suited to maintain a personal webpage and/or to publish your code as tech blogs quickly and efficiently.

* **_Free_** - Hosting is free, all you need is a github account.
* **_Fast_** - It supports Jekyll, a static site generator. Jekyll makes your site load fast - faster than any WordPress site and it handles traffic very well. FYI, [Obama campaign](https://contribute.ofa.us/donation/index-ovf-ec-alt-1.html) used Jekyll and so does Netflix.
* **_Simple_** - No coding required (not even html/css, Jekyll will do it for you), no server maintainence, no setting up domain, and no maintaining database unlike WordPress. There are countless themes openly available to choose from. 
* **_Secure_** - No vulnerability to hacking unless your github account password is hacked.

Git, GitHub and GitHub Pages are not to be confused with each other:
* Git is a version control system that lets you access previous versions of your work you asked git to keep track of. 
* GitHub is a social site that lets people share their work and/or collaborate on projects using git. 
* GitHub Pages lets anyone with an account on GitHub publish their work - code or otherwise. 

In case you are wondering, it is not a prerequisite to learn git or to be active in GitHub to go ahead and make your website. This blog is written keeping in mind someone who is unfamiliar with all of the above. 

Steps:
1. Set up a GitHub account if you dont already have one
2. Create a repository named *your_username.github.io*
3. Publish GitHub Page with URL *http://your_username.github.io*
4. Add content

### Step 1: Sign up for GitHub or log in 
Your username will become part of the url of your website, so it's best to choose one that is concise, memorable and uniquely identifiable to your name. GitHub lets you change username anytime but its [not advisable](https://help.github.com/articles/what-happens-when-i-change-my-username/) later on. 

![]({{ site.url }}/images/GitHubPages/screenshot-1.png){:width="890px"}

### Step 2: Create a repository named *your_username.github.io*
Once you sign up or log in, select "Start a project":

![]({{ site.url }}/images/GitHubPages/screenshot-2.png){:width="890px"}

If you just signed up, GitHub might ask you to first verify your email address before you create the repository.

![]({{ site.url }}/images/GitHubPages/screenshot-3.png){:width="890px"}

The repository name must be in the right format **_your_username.github.io_** for publishing with the GitHub Pages. Select the option "Initialize this repository with a README":

![]({{ site.url }}/images/GitHubPages/screenshot-4.png){:width="890px"}

This is how your repository will look like:

![]({{ site.url }}/images/GitHubPages/screenshot-5.png){:width="890px"}
 
If you forgot to select the option above and a README file is not created, you can create it now with "Create new file" option.

### Step 3: Go to settings, select theme and publish.
First, go to the settings in the top bar of your repository and click on the settings. It will open a page like this:

![]({{ site.url }}/images/GitHubPages/screenshot-6.png){:width="890px"}

Then, scroll down and click on the "Choose a theme" button:

![]({{ site.url }}/images/GitHubPages/screenshot-7.png){:width="890px"}

There are many options, out of which I chose _Tactile theme_:

![]({{ site.url }}/images/GitHubPages/screenshot-8.png){:width="890px"}

Your webpage has been created and you can now check it out at _your_username.github.io_!

### Step 4: The content is added in the ReadMe file. 
The content of the homepage of your site comes from the ReadMe.md file. The file extension .md implies Jekyll would treat the content in the ReadMe file as a markup language. Markup language is an alternative to HTML and it is plain writing with no tags and much simpler syntax for formatting summarized [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

![]({{ site.url }}/images/GitHubPages/screenshot-9.png){:width="890px"}

Once you add and modified the content, the changes are commited in the same way as you would save a file:

![]({{ site.url }}/images/GitHubPages/screenshot-10.png){:width="890px"}

The changes made will be reflected in the website. Sometimes it takes some time and a few more commits for the changes to appear in the website.

![]({{ site.url }}/images/GitHubPages/screenshot-11.png){:width="890px"}

[//]: # (And in the ReadMe.md file:)

The last step of editing the ReadMe.md file can be repeated as many times as the content of the website is built.

Once a basic webpage is set up, there are many interesting ways to polish it based on your needs:  
* Forking from one of the openly available [Jekyll themes](https://github.com/search?utf8=%E2%9C%93&q=jekyll+themes&type=) on Github and working on it to build a customized website (It will be very helpful and perhaps necessary to install and use Jekyll locally on your computer for this and also make use of git).
* Making blog posts.
* Including a comment section, like this blog has [disqus](https://disqus.com/) below.
* Setting up a custom domain.
* Including [MathJax](https://www.mathjax.org/) to typeset mathematical expressions.
* Adding buttons for linking with social media.
* Using [google analytics](https://analytics.google.com/analytics/web/) to track traffic on website.

[//]: # (Some related blogs that I learnt from and find useful:)

Any questions, comments and/or suggestions for future blogs are welcome! If you find this blog useful, the icons below lets you share it in social media.
