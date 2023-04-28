# Proxy vs Reverse Proxy #
1. Types of proxy
	1. Forward proxy
		1. Sits between a group of client machines and the internet
		2. When clients make requests on the internet, forward proxy acts as a middleman
			1. Intercepts requests and talks to the web servers on behalf of the client machines
				1. Why?
					1. Protects client's online identity
						1. IP address of client is hidden from the server
							1. Only the IP address of the proxy is visible (It doesn't allow tracing back to the client)
			2. Can be used to bypass browsing restrictions
				1. Some institutions (Businesses, schools, governments) use firewall to restrict access to the internet
				2. Connecting to the forward proxy outside the firewalls, the client machines can get around the restrictions
					1. However, firewalls can themselves block the connection to the proxy
			3. Can be used to block access to certain content
				1. All connections to the web could be through proxy
				2. Filtering rules are applied to disallow certain sites (social media sites say)
					1. Requires client application to point to it
	2. Reverse proxy