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
* GitHub Pages lets anyone with a github account publish their work - code or otherwise. 

In case you are wondering, its not a prerequisite to learn git or to be active in github to go ahead and make your website. This blog is written keeping in mind someone who is unfamiliar with all of the above. 

Steps:
1. Set up a GitHub account if you dont already have one
2. Create a repository named *your_username.github.io*
3. Publish GitHub Page with URL *http://your_username.github.io*
4. Add content

##### Step 1: Sign up for Github or login 
Your username will become part of the url of your website, so it's best to choose one that is concise, memorable and uniquely identifiable to your name. Github lets you change username anytime but its [not advisable](https://help.github.com/articles/what-happens-when-i-change-my-username/) later on. 

![]({{ site.url }}/images/GitHubPages/screenshot-1.png){:width="720px"}

##### Step 2: The repository name must be in the right format *your_username.github.io* with your current username. Add a `ReadMe.md` file.
![]({{ site.url }}/images/GitHubPages/screenshot-2.png)
If you just signed up, GitHub might ask you to verify your email address before you create the repository.
![]({{ site.url }}/images/GitHubPages/screenshot-3.png)
![]({{ site.url }}/images/GitHubPages/screenshot-4.png)
##### Step 3: Go to settings, select theme and publish.

##### Step 4: The content is added in the ReadMe file. Its simply writing as you would write and commit. Jekyll reads it as a markup language. There are a few things you need to know.

Advanced:
* Customize your website using Jekyll themes.
* Include a comment section, like I am using disqus for this blog.
* Set up a custom domain.
* Use google analytics.

[//]: # (Some related blogs that I learnt from and find useful:)

Any questions, comments and/or suggestions for future blogs are welcome! If you find this blog useful, the icons below lets you share it in social media.
