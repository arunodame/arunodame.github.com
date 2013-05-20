---
layout: blog
title: "Hosting Meteor apps as an client"
category: blog
tags: [meteor]  
summery: A way we can host meteorjs apps as a client and possible use cases
image: /images/blog/telescope-logo.png
---

This is a blog on my another hack into [meteor](http://meteor.com). Before discussing anything just look at this URL - <a href='http://telescope-client.herokuapp.com' target='_blank'>http://telescope-client.herokuapp.com </a>

The app you see is the popular meteor app [telescope](http://telesc.pe). And you saw it is loading from heroku? and it has the all the content of <a href='http://demo.telesc.pe' target='_blank'>http://demo.telesc.pe</a>

## What is happening here

This heroku app simply serve the static files related to telescope demo app. So heroku will be served as file server, nothing more. No websockets or sockjs connections will proxy through heroku.

## How this works

If you skim throught the [`index.html`](https://github.com/arunoda/telescope-client/blob/master/index.html) you'll see all the related `js` and `css` will be loaded from the heroku. And we'll ask meteor to connect with telescope demo app server with [`DDP_DEFAULT_CONNECTION_URL`](http://goo.gl/gopjy) runtime config property.

## What are the usecases

This seems like useless at first. But this is quite powerful and we can do alot with this. Some of them are,

* Use a CDN to serve all the static files
* Use this as a loadbalancer by dynamically changing `DDP_DEFAULT_CONNECTION_URL`
* Inject HTML/JS/CSS (see I've done it with a custom header)

<iframe src="http://ghbtns.com/github-btn.html?user=arunoda&repo=telescope-client&type=watch&count=true&size=large" allowtransparency="true" frameborder="0" scrolling="0" width="125px" height="30px">
</iframe>
<iframe src="http://ghbtns.com/github-btn.html?user=arunoda&repo=telescope-client&type=fork&count=true&size=large" allowtransparency="true" frameborder="0" scrolling="0" width="152px" height="30px">
</iframe>

What you guyes think about this? Do you find this useful? 