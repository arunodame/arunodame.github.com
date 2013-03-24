---
layout: blog
title: Probing CPU & Memory Usage on Nodejitsu
category: blog
tags: [nodejitsu, nodejs]  
summery: Shows how to probe cpu and memory on Nodejitsu right inside the app.
image: /images/blog/nodejitsu-logo.png
---

Last month I released [node-usage](https://github.com/arunoda/node-usage) to probe CPU and Memory information using a valid PID. It was build on top of the `/proc` filesystem on Linux.

Motivation for the `node-usage` was to measure CPU and Memory usage on nodejs cloud platforms. But it didn't work with Nodejitsu because they are using SmartOS (a flavor of Solaris).

Today, I release `node-usage` with solaris compatibility. And now it works on Nodejitsu.

<iframe src="http://ghbtns.com/github-btn.html?user=arunoda&repo=node-usage&type=watch&count=true&size=large" allowtransparency="true" frameborder="0" scrolling="0" width="125px" height="30px">
</iframe>
<iframe src="http://ghbtns.com/github-btn.html?user=arunoda&repo=node-usage&type=fork&count=true&size=large" allowtransparency="true" frameborder="0" scrolling="0" width="152px" height="30px">
</iframe>

See it in action.

<iframe width="560" height="315" src="http://www.youtube.com/embed/zz39GUk4Kec" frameborder="0" allowfullscreen>
</iframe>

[Here](https://github.com/arunoda/node-usage-nodejitsu) is the sample app used on the video.