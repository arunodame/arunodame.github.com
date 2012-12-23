---
layout: blog
title: Github is Down and I can't deploy my app
category: blog
tags: [github, heroku]  
summery: My Heroku app affected recent Github Outage. Here is why?
image: /images/blog/github-outage-logo.jpg
---

>I wrote this post while github is down. But I couldn't make it online at that time since my blog is powered by github pages.

Today(2012 December 23), [Github](https://github.com) is experiencing major [system outage](http://news.ycombinator.com/item?id=4957935). Github has a very good uptime and this is not about them. This is about Heroku. Yes, [Heroku](https://heroku.com). Why? If it is an AWS outage this seems fair :) but how come Github? 

##Here is Why?

I'm using my heroku app with a custom [buildpack for NodeJS](http://arunoda.me/blog/official-nodejs-binaries-on-heroku.html). Since I'm not enjoying with their default NodeJS runtime. And the buildpack is retrieved from github. So now heroku can't access my buildpack and I simply can't deploy.

![Heroku buildpack failed due to github outage](/images/blog/heroku-buildpack-failed.png)

##Okay! Try BitBucket?

Fortunately! Buildpack should be a public git-repo. So I pushed buildpack into BitBucket and tried again. And It works.

![Heroku buildpack works with Bitbucket](/images/blog/heroku-buildpack-with-bitbucket.png)

##But Unfortunately!

Some of the modules used in my app are fetched from Github! I think you know the rest of the story. :) 

I should wait a bit until github comes live again :P

