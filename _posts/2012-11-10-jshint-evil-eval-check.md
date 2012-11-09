---
layout: blog
title: JSHint's evil "eval" check
category: blog
tags: [jshint]  
summery: Possible Bug in JSHint's eval check
image: /images/blog/jshint-logo.jpg
---

Today, when I was building one of of my JavaScript project, it failed suddenly. And the error was a lint error which caused by [JSHint](http://www.jshint.com/) (via [Grunt](http://gruntjs.com/)). It was an `eval` error and I was pretty sure I've not used eval. After looking at the error I found that, it raised because of the following line.

	result =  schemaEvaluator.eval(experimentId, schema);

Here is the Error Message

![JSHint's Evil Eval Check](/images/blog/jshint-eval-error.png)

It seems like JSHint does not parse JavaScript for checking `eval` and possibly others. 

	
