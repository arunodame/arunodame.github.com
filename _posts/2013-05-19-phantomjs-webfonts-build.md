---
layout: blog
title: "PhantomJS with Webfonts Support - Binary Build"
category: blog
tags: [phantomjs]  
summery: Webfonts doesn't get rendered with PhantomJS. But with these custom build binaries it is possible.
image: /images/blog/phantomjs-with-webfonts.jpg
---

[PhantomJS](http://phantomjs.org/) is a Web Browser without a GUI which can be programmable with JavaScript. It is very useful for automated testing, screen capturing, automation and for [so many other use cases](https://github.com/ariya/phantomjs/wiki#learn).

But by default PhantomJS does not work with [WebFonts](http://www.google.com/fonts/). There are [few github issues and fixes](https://github.com/ariya/phantomjs/search?q=web+fonts&type=Issues) regarding this, but it not yet fixed in the core. Fortunately there is a really [nice guide](http://goo.gl/vZErd) about enabling WebFonts support for PhantomJS. It works (atleast for me).

But you've to build it from the source and it takes considerable amount of time. Fortunately (for you) I have already build them for OSX and Linux. So you can directly use following binaries which has WebFonts support.

## [Download PhantomJS 1.9 with WebFont support](https://drive.google.com/folderview?id=0B4Wl57IYdOIPZVl3VFU4TFdVVTg&usp=sharing#list)