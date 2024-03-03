## Long Polling ##
### Advantages ###
1. It is simple to implement
2. Good for small-scale projects
3. Nearly universally supported

### Disadvantages ###
1. Ajax polling adds HTTP overhead since it constantly establishes and tears down HTTP connections
	1. Unnecessary network roundtrips
	2. Unnecessary consumption of CPU
2. Not scalable
3. Reliable message ordering can be an issue for multiple requests
4. Increased latency since server needs to wait for a new request to send a new response

## Server-Sent Events ##
### Advantages ###
1. Designed to be efficient by opening only a single long-lived HTTP connection & server sends events when it has it
	1. Client doesn't request again but waits for messages
2. Well supported in most browsers (Chrome, Edge, Safari, Firefox, Opera, IE, Chrome for Android [http://caniuse.com/#feat=eventsource](http://caniuse.com/#feat=eventsource))
	1. Exception: IE
		1. Solution: Polyfills ([https://github.com/Yaffle/EventSource](https://github.com/Yaffle/EventSource)) & jQuery Plugin ([https://github.com/rwaldron/jquery.eventsource](https://github.com/rwaldron/jquery.eventsource))
3. Simple and clean to implement on the client side and on the server side
4. JSON encoded objects (strings, numbers, arrays, and objects) can be sent which can easily be converted to JavaScript objects
	1. On client side: `JSON.parse()`
	2. PHP: `json_encode()`
5. No trouble with firewalls
6. Great for one-sided server-to-client real-time traffic or for multiple events

### Disadvantages ###
1. Persistent connections can potentially cause many open connections to the server
	1. Solution: Some servers (like Nginx) handle massive number of concurrent connections
2. Does not support binary data
	1. Solution: Encode binary data as a Base64 string on the server side and decode the data on the client side

## Websocket ##
### Advantages ###
1. Full-duplex asynchronous messaging
2. Lightweight for both client and server

### Disadvantages ###
1. Terminated connections are not automatically recovered
2. Older browsers do not support WebSockets
	1. Solution: It is becoming less relevant now

## Implementation Examples ##
1. [https://www.turtle-techies.com/long-polling-vs-server-sent-events/](https://www.turtle-techies.com/long-polling-vs-server-sent-events/)