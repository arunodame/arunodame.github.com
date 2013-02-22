---
layout: blog
title: How to monitor dyno usage on Heroku with NodeJS
category: blog
tags: [heroku, nodejs]  
summery: Deploying on Heroku is easy. But monitoring is super hard/expensive. This is how I overcome that :)
image: /images/blog/heroku-logo-thumb.jpg
---

I don't need to do an introduction to heroku, It's stylish and we could deploy apps in seconds. Recently there are [some rants](http://goo.gl/7Y71e) about the Heroku's routing performance, but it works well for me since I use Heroku with NodeJS. 

But the problem comes when the app on the production. Here are two main problems I came across.

1. How to measure CPU/Memory Usage?
2. How can I auto scale?

Sadly there is no direct answer for this from Heroku. Really! YES YES YES.

But there are some indirect solutions / tricks

### New Relic

We can use [New Relic addon](https://addons.heroku.com/newrelic). This is the best solution from [the community](http://bitly.com/bundles/arunoda/8). But unfortunately, It is still not yet available for NodeJS. 

I've never used New Relic. So I cannot comment on their service. However new-relic's pro plan ask for **~$43** per month, per dyno. It is too expensive, if I just wanted to track CPU Usage and play around with it.

### Nodetime

There is another addon called [Nodetime](https://addons.heroku.com/nodetime) which added recently. It is also same as the above, But works(only) for node.

### Use `/proc/

When I was googling. I found a random [stackoverflow](http://goo.gl/V3p6U) comment, and it said one of the heroku's support staff said to use `/proc/*/statm`. 

What? That's not the Heroku's Style.

## The Solution

I couldn't figure out good solution for this. So I built [node-usage](https://github.com/arunoda/node-usage). A simple, lightweight NodeJS usage tracking module which works on heroku. (and on linux too)

I simply integrated with our metrics tracking tool and, now I can look into my Dyno usage in style. It works pretty well.

## Problems

Heroku's Dyno runs on a shared 32 Gig RAM, Quad Core EC2 Box. RAM is limited to 512 MB, but they never mentioned anything about the CPU on their docs. So, the CPU percentage we got is questionable. But at least there is something we can play around.

## Next - Auto Scaling

Heroku dont do auto scaling yet. But I needed it, so I will use metrics gained from [node-usage](https://github.com/arunoda/node-usage) to build a auto scaling engine for Heroku. I hope to host it on Heroku too. 

Heroku, I love you. Actually I was asked to love by my client :). Please make it better.
