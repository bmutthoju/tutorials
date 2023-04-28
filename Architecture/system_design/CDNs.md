# CDNs #
## How do CDNs work? ##
1. CDN stands for Content Delivery Network, and it is a system that allows for the distribution of content across a network of servers. A CDN works by caching content in multiple locations, such as data centers around the world, and serving that content to users from the server that is geographically closest to them. This can improve the performance and reliability of websites and other online services.
2. Here is how a typical CDN works:
	1. A user requests a piece of content, such as a webpage, image, or video, from a website.
	2. The website's DNS server receives the request and looks up the IP address associated with the requested domain name.
	3. The DNS server returns the IP address of the CDN's server that is closest to the user.
	4. The user's device sends a request for the content to the CDN's server.
	5. The CDN's server checks if it has the content in its cache. If it does, it serves the content directly from its cache.
	6. If the CDN's server does not have the content in its cache, it retrieves the content from the origin server, which is the server that hosts the original content.
	7. The CDN's server caches the content and serves it to the user.
3. By caching content in multiple locations and serving it from the server closest to the user, a CDN can reduce the distance that content has to travel and improve the speed and reliability of content delivery. This is especially important for websites and online services that have users located in different parts of the world.