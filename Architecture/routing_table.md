# Routing Table #
## What are route tables? ##
Route tables are a key component of network routing. They are used by routers and other networking devices to determine the best path for network traffic to reach its destination. A route table is essentially a database of network routes that contains information about the network addresses and subnets that can be reached through a particular network interface or gateway.

In a route table, each entry specifies a destination network address or subnet, along with the gateway or next hop device that should be used to forward traffic to that destination. The route table is consulted by the router or networking device whenever it needs to determine the best path for a packet to reach its destination. The device compares the destination address of the packet to the entries in the route table, and selects the best match based on the most specific matching prefix.

Route tables can be configured manually or automatically, depending on the network topology and requirements. In complex networks, route tables may be updated dynamically using routing protocols such as OSPF, BGP, or IS-IS, which enable routers to exchange information about network topology and routes. This allows routers to build a complete picture of the network and make routing decisions based on real-time information.

Overall, route tables are an essential part of network routing, enabling efficient and reliable communication between devices on a network.

## Give an example of routing table. ##
Sure, here is an example of a routing table:

Network		Destination		Netmask	Gateway		Interface
192.168.0.0	255.255.255.0	192.168.1.1			eth0
10.0.0.0	255.0.0.0		10.1.1.1			eth1
0.0.0.0		0.0.0.0			192.168.1.254		eth0

In this example, we have three rows representing the different routes that traffic can take depending on the destination network.

The first row indicates that traffic destined for the network 192.168.0.0 with a subnet mask of 255.255.255.0 should be routed through the gateway 192.168.1.1 using the interface eth0.

The second row indicates that traffic destined for the network 10.0.0.0 with a subnet mask of 255.0.0.0 should be routed through the gateway 10.1.1.1 using the interface eth1.

The third row is a default route, which indicates that any traffic that does not match the first two rows should be routed through the gateway 192.168.1.254 using the interface eth0.

## How are routing tables populated? ##
Routing tables are populated through a variety of methods, depending on the type of network and the network protocols being used. Here are some common ways that routing tables can be populated:

1. **Static routes**: A **network administrator can manually configure the routing table on each device in the network, specifying which network destinations should be reached through which gateway or interface**.
2. **Dynamic routing protocols**: These are **protocols that allow routers to share information about the state of the network and update their routing tables automatically**. **Examples of dynamic routing protocols include OSPF, RIP, and BGP**.
3. **Default routes**: These are **routes that are used when no specific route is available for a particular destination**. **Default routes can be manually configured or learned through dynamic routing protocols**.
4. **Host routes**: These are **routes that specify a specific host on a network, rather than a network destination**. **Host routes can be added manually or learned through dynamic routing protocols**.

Overall, routing tables are populated through a combination of manual configuration and dynamic updates, allowing network devices to adapt to changes in the network and route traffic efficiently.

## How does OSPF protocol work? ##
**OSPF (Open Shortest Path First) is a dynamic routing protocol** that **uses link-state routing to determine the shortest path between two points in a network**. Here are the basic steps of how OSPF protocol works:

1. **Establishing adjacencies**: **OSPF routers form adjacencies with other routers on the same network segment by exchanging hello packets**. The **hello packets contain information such as the router ID, the network mask, and the priority of the router**.
2. **Building the topology database**: **Once the adjacencies are established, the routers exchange link-state advertisements (LSAs) that describe the state of their connected links**. **Each LSA contains information about the router's interfaces, the networks connected to those interfaces, and the cost (or metric) of reaching those networks**.
3. **Calculating the shortest path tree**: **OSPF routers use** the **information from the LSAs to build a complete picture of the network topology, which is stored in a database called the OSPF link-state database (LSDB)**. **Using the LSDB, each router calculates the shortest path tree (SPT) to every other router in the network**. The SPT is calculated **using Dijkstra's algorithm, which takes into account the cost of each link between routers**.
4. **Advertising routes**: **Once the SPT is calculated, each router advertises its routes to other routers in the network using OSPF packets called updates**. The **updates contain information about the destination network, the cost of reaching that network, and the next-hop router**.
5. **Maintaining the database**: **OSPF routers continually exchange hello packets and update LSAs to keep the link-state database up-to-date with any changes in the network topology**. **If a link or router fails, OSPF routers detect the failure and update their LSAs accordingly, triggering a recalculation of the SPT**.

Overall, OSPF is a robust and efficient routing protocol that scales well to large and complex networks. By using link-state routing and building a complete picture of the network topology, OSPF can calculate the most efficient paths between routers and adapt to changes in the network quickly and accurately.