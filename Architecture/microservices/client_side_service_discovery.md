# Client-Side Service Discovery #
## How does client-side service discovery work with a feign client? ##
Feign is a popular **Java-based HTTP client library** that simplifies the process of making HTTP requests to external services. When it comes to **client-side service discovery**, **Feign relies on an external service registry, such as Consul or Eureka, to obtain the necessary information about the services it needs to communicate with**.

Here is an **overview of how client-side service discovery works with a Feign client**:

1. The **Feign client sends a request to an external service using the service's logical name, rather than its physical address**. This **logical name corresponds to a service definition in the service registry**.
2. **Before sending the request, Feign consults the service registry to obtain the physical address of the service**. The **registry provides the necessary information, such as the service's IP address and port number**.
3. **Feign then sends the request to the physical address obtained from the service registry**. This **allows Feign to communicate with the external service, without needing to know the service's specific network details**.
4. **If the external service's physical address changes, the service registry is updated accordingly**. **Feign can then obtain the new address information from the registry, allowing it to continue communicating with the service, even if the underlying network configuration has changed**.

Overall, client-side service discovery with Feign allows for greater flexibility and resilience when communicating with external services. By **relying on a centralized service registry, Feign can adapt to changes in the network configuration, without requiring any modifications to the underlying codebase**.

## How does feign load-balancing work? ##
Feign itself does not include a built-in load-balancing mechanism. Instead, **it relies on external load-balancing tools, such as Ribbon or Eureka, to distribute requests across multiple instances of a service**.

Here is **an overview of how Feign load-balancing works with Ribbon and Eureka**:

1. **Ribbon is a client-side load-balancer that is integrated with Feign**. It is **responsible for distributing incoming requests across multiple instances of a service, based on a specified load-balancing strategy**.
2. **Feign uses Ribbon to obtain the physical address of a service instance from the service registry, and then sends the request to that address**.
3. **If** the **load-balancing strategy used by Ribbon is "round-robin"**, for example, then **each successive request will be sent to a different service instance in a cyclical manner**. **Other load-balancing strategies**, such as **"least-connections"** or **"random"**, are also available.
4. **Ribbon continuously monitors the health of each service instance, and removes any instances that are not responding or are performing poorly from the list of available instances**. This **ensures that requests are only sent to healthy and responsive instances of the service**.
5. **Eureka is another service discovery and registration tool that can be used with Feign**. **When Feign is configured to use Eureka, it automatically obtains the list of available instances for a service from the Eureka server, and uses Ribbon to distribute requests across those instances**.

Overall, Feign load-balancing with Ribbon or Eureka provides a convenient and flexible way to distribute requests across multiple instances of a service, without requiring any manual configuration or management.

## What is the flow with feign client, ribbon, and Eureka server? ##
The flow with Feign client, Ribbon, and Eureka server is as follows:

1. When a **client application** needs to communicate with an external service, it **uses a Feign client to make HTTP requests to the service**. The **client specifies the logical name of the service, rather than its physical address**.
2. The **Feign client then uses Ribbon to obtain the physical address of the service from the service registry, such as Eureka**. **Ribbon consults the registry to obtain a list of available instances for the service, and uses a load-balancing strategy to distribute requests across those instances**.
3. **Ribbon monitors the health of each instance, and removes any instances that are not responding or are performing poorly from the list of available instances**. This **ensures that requests are only sent to healthy and responsive instances** of the service.
4. **If** the **service instance is not found in the local cache, Ribbon communicates with the Eureka server to obtain the list of available instances for the service**.
5. **Once Ribbon has obtained the physical address of a service instance, the Feign client uses that address to make an HTTP request to the service**.
6. **If** the **address of the service instance changes, the service registry, such as Eureka, is updated accordingly**. **Ribbon is then notified of the change, and can obtain the new address information from the registry, allowing it to continue distributing requests to the updated set of instances**.

Overall, the combination of Feign client, Ribbon, and Eureka server provides a powerful and flexible way to implement client-side service discovery and load-balancing in a distributed system. It allows client applications to communicate with external services in a transparent and resilient manner, without being tied to specific network details or configurations.