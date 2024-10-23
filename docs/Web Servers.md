> 📝️ **Video Transcript**: This is the transcript for a video on my youtube channel. It should still be just as readable as an article, but you can also see the video [Web Servers and Rise of Javascript and NodeJS](https://www.youtube.com/watch?v=drhZlg5AtYs).

### Overview

To understand modern web servers and rise of dynamic applications with asynchronous Javascript, we have to understand the web before any such thing existed and to find a point in history to begin.   

Since a comprehensive history of the web would require going back 30 plus years to the original invention of the world wide web, early browsers such as Mosaic, Netscape, and even more ancient web servers, we will begin in 1995 with the release of Apache HTTPd, which after nearly 3 decades, still powers over 23% of the top million busiest websites.

### Apache

The original Apache developers, started as a group of webmasters, now an outdated term, at the National Center for Super computing Applications or NSCA, where much of the pioneering of the early internet began. The previous web server NCSA HTTPd, needed several patches and improvements, and eventually, Apache was built as a general overhaul and redesign. Still, 30 years later, the main function of serving static HTML files to clients hasn't changed. Over HTTP, or hyper-text-transfer-protocol, a client, aka web browser, issues a GET-request and a server responds with HTML files and other resources that make up the web page presented to the user.

For this simple purpose, Apache did great, however, with the growing popularity of the internet, and more and more people watching porn, looking at cat pictures, and ordering dog food, the issue of scalability arose. A single server running can only handle so many requests per second as well as concurrent connections. This become known as the C10K problem, the major challenge for computing in the late 90s and early 2000s where handling over 10 thousand concurrent connections was impossible. Only one man was capable of solving this problem, a Russian system administrator by the name of Igor Syostev. 

### Nginx

Responsible for running servers for the top websites in Russia at the time, as well as Rambler, a Russian search engine and web portal, Igor experienced the scalability issues of Apache first hand. In his spare time, he began writing drafts for NGINX in 2002, focusing on handling many simultaneous connections with an asynchronous event driven approach. After 2 years, it was publically released in 2004. Fast forward to 2019 and 66% of top 10k sites use NGINX according to W3 Techs. There are of course several other roles it plays besides serving static content such as HTML and other resources to clients. One, being a reverse proxy, which acts as a gateway between the mass of clients and web servers. This acts as an intermediary load balancer that also can enforce security by directing traffic through firewalls.

With Apache and Nginx being used primarily as web servers at the time, Javascript and event driven programming was growing in popularity. Despite this, sequential programming and blocking I/O was still a problem with web servers. For example if a server is waiting for one function of code to finish, this may block user requests or database queries, slowing an application down. Inspired by Nginx, American software engineer Ryan Dahl had a solution: a vision of a purely event driven, non-blocking web server. 

### NodeJS

Ryan was inspired by Nginx and suggests scenarios where they could be used together, Apache on the other hand he criticized for it's limited design where an entire thread is created per connection.

Ryan explains pitfalls of blocking, sequential programming and cultural bias where functions with callbacks are seen as too complicated and as nested "spaghetti code" in this [excerpt](https://www.youtube.com/watch?v=M-sc73Y-zQA&t=836s).

Though Node JS has proven to be highly performant and reliable, it may come at a cost of complexity and code readability, with many preferring threaded servers and sequential code where you can easily read a file top to bottom without jumping between Javascript's callback functions.

After these early criticisms of Javascript, there were improvements such as Promises in 2015 with the release of ES6. Promises are a abstraction build on top of callbacks to better handle async code and prevent callback hell. Finally the latest evolution is async/await which is essentially syntactic sugar for promises, completely optional and fully compatible with promises.

So clearly, the history of asynchronous JavaScript is a bit messy, but that's the story of any technology that's been around for 25 plus years in an ever changing landscape such as the web.

Besides the async/await pattern found in almost every major language today, another model of concurrency that seems promising is in the Go programming language with it's goroutines and channels which has proven useful in modern web servers in recent years. But that's a topic another video.

Thank you for watching and don't forget to like, comment and subscribe to support more content like this.

### Additional Unorganized Notes Or Not Included In Video

So to wrap everything up, the earliest web server still in wide use today is Apache, which saw limitations in scalability, known as the C10K problem, NGNIX came as a solution with it's asynchronous, even driven approach. As the web evolved, the demand for... interactive web pages, non-blocking, 

Explain promises and then async/await a bit more. Then summarize everything, maybe somehow slip in Go's concurrency compared to async await. Perhaps hype up some a concurrency model different than async/await created from the greatest engineers in the world who created C and Unix, just mention it and then leave them on a cliffhanger and say that will be a future video. 

#### Additional Notes

2012: Apache 2.4 released with larger selection of MPMs, reverse proxy impovements, and additional load balancing mechanism according to [Timeline](https://nickvidal.github.io/httpd25/)

Apache has Prefork and Worker MPM (Multi Processing Module)

Though primarily a Javascript runtime, like the JVM is for Java, or CPython is to Python, NodeJS can be used to create a web server, and very often is. And in that sense, comparable to Apache and Nginx.
	
For serving static content, Apache or NGINX do fine on their own, for dynamic server-side functionality like interacting with databases, or a real time chat application, Node shines best. 

Sometimes Node and Nginx can be used together, which node containing the code base of an application, while Nginx sits infront handling load balancing and caching.

Ryan Dahl in 2010: "Apache creates a thread per connection" [link](https://youtu.be/M-sc73Y-zQA?t=578)

What is the difference between nodejs and nginx? See Reddit post.
[NodeJS vs Nginx Reddit](https://www.reddit.com/r/node/comments/1b2y6ep/what_is_the_difference_between_nodejs_and_nginx/)
