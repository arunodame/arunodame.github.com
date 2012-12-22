---
layout: blog
title: Official NodeJS Binaries on Heroku
category: blog
tags: [heroku, nodejs]  
summery: Use Official NodeJS Binaries on Heroku. Even supports unstable versions.
image: /images/blog/heroku-logo-thumb.jpg
---
<iframe src="http://ghbtns.com/github-btn.html?user=arunoda&repo=heroku-nodejs-binary-buildback&type=watch&count=true&size=large"   allowtransparency="true" frameborder="0" scrolling="0" width="125px" height="30px">
</iframe>
<iframe src="http://ghbtns.com/github-btn.html?user=arunoda&repo=heroku-nodejs-binary-buildback&type=fork&count=true&size=large"   allowtransparency="true" frameborder="0" scrolling="0" width="152px" height="30px">
</iframe>

[NodeJS](http://nodejs.org) support for [Heroku](http://heroku.com) is pretty cool. They support node from 0.4.x to 0.8.x. But they don't have the latest node version or it takes few weeks to arrive. And they don't have unstable node version support either.

For most of the apps, this is not a problem. But for some, it is problem. I've encountered such a situation and I needed latest `node` and the latest `node-gyp`. It is not possible to have these on heroku for nodejs.

## But wait! Heroku has build-packs

Heroku is a [polyglot platform](http://blog.heroku.com/archives/2011/8/3/polyglot_platform/) and theoretically they support any language and framework. They do it via [build-packs](https://devcenter.heroku.com/articles/buildpacks). Build Pack is a set of BASH scripts which builds a given app.

I've created build a Build Pack for Heroku using [Official NodeJS Binaries](http://nodejs.org/download/) for Linux. Now we can use any version of NodeJS which is available on [nodejs.org/dist](http://nodejs.org/dist/).

>Note: Official NodeJS Binaries for Linux only available from v0.8.6

##Usage

###For a new app

    $ heroku create --stack cedar --buildpack https://github.com/arunoda/heroku-nodejs-binary-buildback.git
    $ git push heroku master

###For an existing app

    $ heroku config:add BUILDPACK_URL=https://github.com/arunoda/heroku-nodejs-binary-buildback.git
    $ git push heroku master

Using Custom NodeJS version
---------------------------

**Only for versions >= 0.8.6**

    $ heroku labs:enable user-env-compile -a <app_name>
    $ heroku config:add NODE_VERSION=<node_version>
