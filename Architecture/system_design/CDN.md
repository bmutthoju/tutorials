# What is a CDN? How Does it Work? #
1. Content Delivery Network:
	1. Originally developed to speed up delivery of static HTML content for users all around the world
	2. A CDN brings content closer to the user
		1. This improves performance of the web-service (as percieved by the user)
	3. To bring a server close to the user, CDN is deploys servers at 100s of locations
		1. The servers are called: Point of Presense (PoP)
			1. Aka Edge Servers
		2. A user can reach an edge server close to him/her
	4. Technologies:
		1. Amazon Cloudfront
		2. Cloudflare
		3. Akamai
		4. Microsoft Azure CDN
	5. Techniques:
		1. **DNS based routing**
			1. Each PoP has its own IP address
				1. When a user looks up the IP address for the CDN, DNS returns the IP address closest to the user
		2. Anaycast
			1. All PoPs share the IP address
			2. When a request comes into Anycast network for the IP address
				1. Network sends request to the server that is closest to the user
	6. Each edge server acts as a reverse proxy
		1. Static contents are cached in the edge servers
			1. If a user requests for the content
			2. If the content is in ethe edge server content cache, it is returned
			3. If the content is not in the edge server, it is fetched from the origin server
				1. Advantage: Reduces load and bandwidth requirements of the origin server cluster
2. Features of modern CDNs
	1. Can transform static content into more optimized formats
		1. Examples:
			1. .js, .css -> minified files
			2. images -> 
				1. WEBP (modern image format) (?)
					1. WEBP is an image format developed by Google in 2010 as **a new open standard for web graphics**. It **uses both lossy and lossless compression techniques to reduce the file size of images without compromising the quality of the image**. **WEBP files typically have a smaller file size than JPEG and PNG files**, which can lead to **faster loading times for web pages and reduced bandwidth usage**.
					2. WEBP supports transparency and animation, and it can be used for static images, animated images, and even for displaying transparent images over a background. The format is supported by major web browsers, including Chrome, Firefox, and Microsoft Edge, and it is gaining popularity as a preferred format for web graphics.
					2. Combines compression ability of JPEGs with the quality retention of PNGs and transparency of PNGs
						1. WEBP allows us to make high quality images that are small
					3. https://developers.google.com/speed/webp
						1. WebP lossless images are 26% smaller in size compared to PNGs. WebP lossy images are 25-34% smaller than comparable JPEG images at equivalent SSIM quality index.
						2. caniuse.com
							1. Check compatibility
				2. AVIF
					1. AVIF, short for AV1 Image File Format, is a new open-source image format developed by the **Alliance for Open Media (AOM), a group that includes major tech companies such as Google, Apple, and Amazon**. **It is based on the AV1 video codec and uses the same compression technology to achieve high-quality image compression with smaller file sizes than JPEG and even WEBP**.
					2. **AVIF supports both lossy and lossless compression and has a wide color gamut, allowing for high-quality images with more vibrant colors**. It **also supports alpha channels for transparency and can include animated sequences**. The format is still relatively new and not yet widely supported by web browsers, but it is expected to become more popular as more companies adopt the technology.
					3. One of the main advantages of AVIF is that it can achieve better compression efficiency than existing image formats, resulting in smaller file sizes while maintaining image quality. This means that web pages can load faster and consume less bandwidth, leading to a better user experience for website visitors.
			2. Video -> HD (720p), 2K (1152p), HD (1080p), 4k (2160p)
	2. All TLS connections terminate at the edge server
		1. TLS handshakes are expensive
			1. Needs several roundtrips to establish
		2. TLS termination at the edge significantly reduces the latency
	3. Dynamic content can also be sent to the CDN
3. Benefits:
	1. Security:
		1. All CDNs have huge network capacity at the edge
			1. Can provide DDOS protection against large scale attacks
				1. Network capacity is much larger than the attackers
					1. Anycast network: **Diffuses attack traffic over a huge number of servers**
	2. A modern CDN improves availability
		1. It is highly distributed
			1. Multiple copies allows many hardware failures
4. Good for HTTP traffic

## How does the anycast network work? ##
An anycast network is a network topology in which data is sent to any one of several destinations, but only the nearest or most efficient node receives and processes the data. In other words, anycast allows multiple devices to share the same IP address, and when a packet is sent to that IP address, the network will automatically route the packet to the nearest available node.

In an anycast network, each node has a unique IP address assigned to it, but all nodes share the same anycast address. When a client sends a packet to the anycast address, the packet is routed to the nearest node based on network routing protocols. This allows for more efficient routing of data, as packets are sent to the node that is closest or has the least network congestion.

Anycast is commonly used in distributed computing environments, such as Content Delivery Networks (CDNs), Domain Name System (DNS) servers, and Routing Information Protocol (RIP) routers. In a CDN, anycast is used to distribute content to the nearest server based on the client's location, which reduces latency and improves performance. In a DNS server, anycast is used to route DNS queries to the nearest DNS server, which reduces network traffic and improves response times. In a routing protocol, anycast is used to route traffic to the nearest router that can provide routing information.

Overall, anycast is a powerful networking technology that allows for more efficient routing of data, reducing latency and improving network performance. However, it does require careful planning and configuration to ensure that packets are routed to the correct node, and can also introduce some additional complexity to network design and troubleshooting.

## How is the anycast network implemented? ##
An anycast network is typically implemented using routing protocols that allow multiple devices to share the same IP address. Here is a high-level overview of the implementation process:

1. **Assign a unique IP address to each node**: Each node in the anycast network must have a unique IP address assigned to it. These IP addresses can be assigned manually or automatically using a Dynamic Host Configuration Protocol (DHCP) server.
2. **Advertise the anycast address using routing protocols**: The anycast address is advertised to the network using a routing protocol such as **Border Gateway Protocol (BGP)** or **Intermediate System to Intermediate System (IS-IS)**. The **anycast address is advertised as a normal route with a special attribute that identifies it as an anycast address**.
3. **Configure the routing protocol to select the closest node**: The **routing protocol is configured to select the closest node based on a variety of factors such as network topology, distance, and congestion**. This **ensures that packets are routed to the nearest node and that the network load is balanced across all nodes**.
4. **Configure the nodes to process the anycast address**: **Each node in the anycast network must be configured to process packets sent to the anycast address**. This **involves configuring the network stack to listen for packets sent to the anycast address and to respond to these packets as appropriate**.
5. **Monitor the network for performance and issues**: Once the anycast network is up and running, it is important to monitor it for performance and issues. This **includes monitoring the routing protocols for any changes, monitoring the network traffic to ensure that packets are being routed to the correct node, and troubleshooting any issues that arise**.

Overall, implementing an anycast network requires careful planning and configuration to ensure that packets are routed to the correct node and that the network load is balanced across all nodes. However, once implemented, anycast can provide significant benefits in terms of improved network performance and reduced latency.

## What anycast network libraries or frameworks can be used along with Spring? ##
There are several anycast network libraries and frameworks that can be used along with Spring to implement anycast networking. Here are a few examples:
1. **Netflix Eureka**: Eureka is **a service registry and discovery server that allows services to register and discover each other using a REST API**. Eureka **supports anycast networking, which allows multiple instances of the same service to share the same IP address**.
2. **Consul**: Consul is **a service mesh solution that provides service discovery, health checking, and distributed key-value storage**. Consul **supports anycast networking, which allows multiple instances of the same service to share the same IP address**.
3. **Kubernetes**: Kubernetes is **a container orchestration platform that provides service discovery, load balancing, and scaling capabilities**. Kubernetes **supports anycast networking, which allows multiple instances of the same service to share the same IP address**.
4. **Apache ZooKeeper**: ZooKeeper is **a distributed coordination service that provides configuration management, synchronization, and naming services**. ZooKeeper **supports anycast networking, which allows multiple instances of the same service to share the same IP address**.

These anycast networking libraries and frameworks can be integrated with Spring using various approaches, such as REST APIs, Java libraries, and configuration files. For example, **Netflix Eureka can be integrated with Spring using the Spring Cloud Netflix library, which provides a set of Spring Cloud annotations and interfaces for registering and discovering services with Eureka**. Similarly, **Consul can be integrated with Spring using the Spring Cloud Consul library, which provides a set of Spring Cloud annotations and interfaces for registering and discovering services with Consul**.

## How to configure a network to support anycast routing? ##
Configuring a network to support anycast routing requires coordination with your network administrators, and the specific steps may vary depending on the network equipment and software being used. However, here are some general steps to configure a network to support anycast routing:
1. Enable anycast support on the network equipment: Anycast support must be enabled on the network equipment that will be used to route traffic to the anycast IP address. This includes routers, switches, load balancers, and other networking devices.
2. Configure anycast IP address: Choose an IP address that will be used for anycast routing and assign it to the network interface of each server that will be providing the anycast service. The same IP address will be advertised from multiple locations in the network.
3. Advertise anycast IP address from multiple locations: The anycast IP address must be advertised from multiple locations in the network, so that traffic can be routed to the nearest instance of the service. This can be done using a routing protocol such as Border Gateway Protocol (BGP).
4. Monitor anycast traffic: It is important to monitor anycast traffic to ensure that it is being routed correctly and to detect any issues that may arise. Network monitoring tools can be used to track traffic patterns and identify potential problems.

By following these steps, you can configure a network to support anycast routing, which allows traffic to be routed to the nearest instance of a service, improving performance and availability.

## What is the BGP protocol? ##
The Border Gateway Protocol (BGP) is a **standardized exterior gateway protocol used for exchanging routing information between different autonomous systems (ASes) on the Internet**. It is a **path-vector protocol that is used to determine the best path for traffic to flow from one AS to another**.

**BGP is a complex protocol that is used by Internet service providers (ISPs) and large organizations to route traffic between different networks**. It is **designed to handle a large number of routes and to be scalable, making it suitable for the Internet's massive scale.

The **BGP protocol works by exchanging information about the networks that each AS is responsible for and the paths that traffic can take to reach those networks**. **BGP routers use this information to build a routing table that determines the best path for traffic to flow between different networks**.

BGP is an **important protocol for ensuring the stability and reliability of the Internet**. It is **used to prevent routing loops, to ensure that traffic is routed efficiently, and to prevent the propagation of incorrect routing information**. BGP is **also used to implement traffic engineering, allowing network operators to control the flow of traffic between different networks**.