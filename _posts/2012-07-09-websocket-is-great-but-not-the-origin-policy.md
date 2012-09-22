---
layout: blog
title: WebSocket is great! But not the origin policy
category: blog
tags: [WebSocket]  
summery: "Websocket is great. But it is using Origin policy to make it secure. But it cannot secure it. So we don't need origin policy"
image: /images/blog/websocket-logo.jpeg
---

>**EDIT**
>
>Although Origin header can be spoofed, it helps against [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) attacks. See below and [Hacker News thread](http://news.ycombinator.com/item?id=4215483) for the comments. 

Today, I was looking at WebSocket Specification. I was looking for a way to secure WebSocket. I found something interesting on their [Protocol Specification](http://tools.ietf.org/html/rfc6455).

##Security with WebSocket

AFAIK the only built in way to secure WebSocket is via **origin policy**. Something similar used in [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing). This is how it works according to the spec.

* Client(Web Browser) sends a header called "Origin" with the domain name of the website
* It is send in the initial handshake
* Server can look at this header and allow the request or not

##Some facts on Origin Policy
I've extracted some facts about Origin Policy from the Current Version of Web Sockets [Protocol Specification - RFC6455](http://tools.ietf.org/html/rfc6455)

### Fact #1
Origin header is optional, But it is sent by all the browsers which supports WebSocket

### Fact #2
Server can't verify the Origin Header, because it just a header. Malicious client can create a forge header and send to the server. Here is how spec is looking at that. They are correct.

	While this protocol is intended to be used by scripts in web pages,
	it can also be used directly by hosts.  Such hosts are acting on
	their own behalf and can therefore send fake |Origin| header fields,
	misleading the server.  Servers should therefore be careful about
	assuming that they are talking directly to scripts from known origins
	and must consider that they might be accessed in unexpected ways.  In
	particular, a server should not trust that any input is valid.
([link to the specification](http://tools.ietf.org/html/rfc6455#section-10.1))

### Fact #3
It also said that, Server SHOULD verify the Origin If they need to filter requests.

	Servers that are not intended to process input from any web page but
	only for certain sites SHOULD verify the |Origin| field is an origin
	they expect.  If the origin indicated is unacceptable to the server,
	then it SHOULD respond to the WebSocket handshake with a reply
	containing HTTP 403 Forbidden status code.
([link to the specification](http://tools.ietf.org/html/rfc6455#section-10.2))

[link to the specification - see no.7](http://tools.ietf.org/html/rfc6455#section-4.2.1)

## My Conclusion

* There is no way to verify the authenticity of the **Origin** header
* It is supported by all the browsers which support WebSocket, but anyone can forge it
* **Origin Policy** cannot do anything to make the WebSocket secure
* So It's upto you to make your own security model for your WebSocket based app

