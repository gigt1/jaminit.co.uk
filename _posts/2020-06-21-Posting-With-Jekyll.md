---
categories: [Websites]
tags: [Website, Web Development]
---

[Jekyll](https://jekyllrb.com/) is a static site generator for creating any type of site from blogs like this one to portfolio's or enterprise sites. It doesn't require a database and generates HTML files instead of generating dynamic sites that use php (like [wordpress](wordpress.org)).
# Why use Jekyll
## Ease of use
One of the main reasons that Jekyll is amazing is that it is super easy to setup and develop on. To install you simply need to install the Jekyll Package (```gem install bundler jekyll```) or even easier simply just put your files in a Github Repo and use [Github Pages](https://pages.github.com/).
## Simplicity
Jekyll makes it easy to create sites, it doesn't require MYSQL databases like WordPress and doesn't require setting up complex access rights or managing users. You can write your pages in markdown or html. For simplicity I like to use markdown. Its a really easy language to use and you can use it to build sites without the hassle of having to write HTML.
## Speed
Jekyll is a "static site generator" which as I said earlier generates HTML files. The advantage of this is that it means you're site will load a lot quicker for visitors. The problem with WordPress is that it uses PHP which is a great programming language but runs server side inside of client side, this means everytime someone requests a page on your site it has to be run on your server first, this is problematic when you are getting lots of visitors to your site every second.
# How to make a site in Jekyll
## Setting up
1) First of all you need to [https://jekyllrb.com](https://jekyllrb.com/) where you can visit the quick-start instructions. Here it gives you some commands to quickly install Jekyll. Please note that this step requires you already have Ruby installed (you can do so [here](https://www.ruby-lang.org/en/downloads/)).  
2) Now you've run the commands on the quick-start guide you already have a site setup with the default theme. The `_posts` directory contains all your posts and the root of your folder contains all your pages and config files.
## Creating a post
1) If we want to create a post we first have to use the correct file format, the file format is as follows: `YEAR-MONTH-DATE-Slug-Of-Post.md`. Obviously replace Year Month and Date with the correct information.  

2) Next we need to add the information at the start of the document. We need to add the author information and title. This will depend on the theme also but if you are using the default theme this is what we will use. We add this information by putting: `author: YOUR Name` and `title: The title of your article`, we also surround this with three dashed lines. Your file should now look like this:  
```
---
author: James Cook
title: Making a Jekyll sites
---
```
After this we can simply write our post content in markdown, if you want to learn markdown you can do [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).  
![An example markdown site](/images/Example-Markdown-File.png)  
Above: An example file written in markdown.  
3) Finally we will want to publish our site, this means we need to build our site and convert the files from markdown to HTML. Simply just open your terminal, go to the directory that your Jekyll site is in and run the following:
```
$ Bundle install
$ Jekyll build
```
If you've followed the tutorial correctly you will be then left with a new folder called `_site` simply upload all the files onto your webserver and you're done!
