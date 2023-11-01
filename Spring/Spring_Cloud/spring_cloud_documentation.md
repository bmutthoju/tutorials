# Spring Cloud #
## Overview ##
1. Used to build common patterns in distributed systems
    1. Configuration management
    2. Service discovery
    3. Circuit breakers
    4. Intelligent routing
    5. Micro-proxy
    6. Control bus
    7. One-time tokens
    8. Global locks
    9. Leadership election
    10. Distributed sessions
    11. Cluster state
2. Used to stand up services and applications that implement distributed systems coordination boilerplate patterns.
3. Multi-platform
    1. Local laptops
    2. Bare metal data centres
    3. Managed platforms (Cloud foundary, ...)

## Features ##
1. Out of box solutions for typical use-cases and extensibility mechanisms for others
2. Features:
    1. Distributed/versioned configuration
    2. Service registry and discovery
    3. Routing
    4. Service-to-service calls
    5. Load balancing
    6. Circuit breakers
    7. Global locks
    8. Leadership election and cluster state
    9. Distributed messaging

## Getting Started ##
### Generating a New Spring Cloud Project ###
1. [start.spring.io](start.spring.io)
    1. Select Spring Boot version
    2. Select Spring Cloud projects we want
        1. Adds Spring Cloud BOM version (?) to Maven/Gradle file when project is generated

### Adding Spring Cloud to an Existing Spring Boot Application ###
1. Steps:
    1. Determine the Spring Cloud version to use
        1. Depends on Spring Boot version
            1. Mapping:
                1. Kilburn: 3.0.x, 3.1.x
                2. Jubilee: 2.6.x, 2.7.x
                3. Ilford: 2.4.x, 2.5.x
                4. Hoxton: 2.2.x, 2.3.x
                5. Greenwich: 2.1.x
                6. Finchley: 2.0.x
                7. Edgware: 1.5.x
                8. Dalston: 1.5.x
        2. SR: Service Release:
            1. Bug fixes
            2. Backwards compatible features
                1. Use the latest SR for the service train
                    1. [release notes page](https://github.com/spring-cloud/spring-cloud-release/wiki)
    2. Add Spring Cloud BOM to the application:

            <properties>
                <spring-cloud.version>2022.0.1</spring-cloud.version>
            </properties>
            <dependencyManagement>
                <dependencies>
                    <dependency>
                        <groupId>org.springframework.cloud</groupId>
                        <artifactId>spring-cloud-dependencies</artifactId>
                        <version>${spring-cloud.version}</version>
                        <type>pom</type>
                        <scope>import</scope>
                    </dependency>
                </dependencies>
            </dependencyManagement>

        1. `spring-cloud-dependencies` and `spring-cloud-starter-parent`
            1. `dependencies` version is BOM only version
    3. We can include starters that we can add as dependencies to add various cloud native features to the project
        1. Starter names are documented in individual projects
        2. Example:

                <dependencies>
                    <dependency>
                        <groupId>org.springframework.cloud</groupId>
                        <artifactId>spring-cloud-starter-config</artifactId>
                    </dependency>
                    <dependency>
                        <groupId>org.springframework.cloud</groupId>
                        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
                    </dependency>
                </dependencies>

### Getting Started Resources ###
1. [Beginner's Guide to Spring Cloud](https://www.youtube.com/watch?v=aO3W-lYnw-o)

## Main Projects ##
### Spring Cloud Config ###
1. [https://spring.io/projects/spring-cloud-config](https://spring.io/projects/spring-cloud-config)
2. Centralized external configuration management backed by git repo
3. Config resources map to Spring `Environment` but could be used by non-Spring apps

### Spring Cloud Netflix ###
1. [https://spring.io/projects/spring-cloud-netflix](https://spring.io/projects/spring-cloud-netflix)
2. It is an integration with Netflix OSS components (Eureka, Hystrix, Zuul, Archaius, ...)

### Spring Cloud Bus ###
1. [https://spring.io/projects/spring-cloud-bus](https://spring.io/projects/spring-cloud-bus)
2. It is an event bus that links services and service instances together with distributed messaging
    1. It can be used for propagating state across a cluster (eg. config change events)

### Spring Cloud Open Service Broker ###
1. [https://spring.io/projects/spring-cloud-open-service-broker](https://spring.io/projects/spring-cloud-open-service-broker)
2. It provides a starting point for building a service broker that implements the **Open Service Broker API**

### Spring Cloud Consul ###
1. [https://spring.io/projects/spring-cloud-consul](https://spring.io/projects/spring-cloud-consul)
2. It provides service discovery and configuration management with Hashicorp Consul.

### Spring Cloud Sleuth ###
1. [https://spring.io/projects/spring-cloud-sleuth](https://spring.io/projects/spring-cloud-sleuth)
2. It provides distributed tracing for Spring Cloud applications
3. It is compatible with Zipkin, HTrace, and log-based (e.g. ELK) tracing

### Spring Cloud Data Flow ###
1. [https://spring.io/projects/spring-cloud-dataflow](https://spring.io/projects/spring-cloud-dataflow)
2. A cloud-native **orchestration service** on composible microservice applications on modern runtime [environments]
3. Features that simplify orchestration of microservice based data pipelines:
    1. Easy to use DSL
    2. Drag and drop GUI
    3. REST APIs

### Spring Cloud Stream ###
1. [https://spring.io/projects/spring-cloud-stream](https://spring.io/projects/spring-cloud-stream)
2. It is a light-weight event-driven microservices framework to quickly build applications **that can connect to external systems**
3. Features:
    1. Simple declarative model to send and receive messages between Spring Boot apps using
        1. Apache kafka
        2. Rabbit MQ

### Spring Cloud Stream Applications ###
1. [https://spring.io/projects/spring-cloud-stream-applications](https://spring.io/projects/spring-cloud-stream-applications)
2. They are out of the box Spring Boot applications providing integration with external middleware systems such as Apache Kafka, RabbitMQ etc. using **binder abstraction in Spring Cloud Stream**.

### Spring Cloud Task ###
1. [https://spring.io/projects/spring-cloud-task](https://spring.io/projects/spring-cloud-task)
2. They are short-lived microservices framework to quickly build applications that perform finite amounts of data processing
3. They are simple and declarative used for adding functional and non-functional features to Spring Boot apps.

### Spring Cloud Task App Starters ###
1. [https://spring.io/projects/spring-cloud-task-app-starters](https://spring.io/projects/spring-cloud-task-app-starters)
2. They are Spring Boot applications that may be any process (including Spring Batch jobs) that do no run forever, and they end/stop after a finite period of data processing.

### Spring Cloud Zookeeper ###
1. [https://spring.io/projects/spring-cloud-zookeeper](https://spring.io/projects/spring-cloud-zookeeper)
2. It provides service discovery and configuration management with Apache Zookeeper.

### Spring Cloud Contract ###
1. [https://spring.io/projects/spring-cloud-contract](https://spring.io/projects/spring-cloud-contract)
2. It is an umbrella project which holds solutions that help users in implementing Consumer Drive Contracts approach.

### Spring Cloud Gateway ###
1. [https://spring.io/projects/spring-cloud-gateway](https://spring.io/projects/spring-cloud-gateway)
2. It is an intelligent and programmable router based on Project Reactor.

### Spring Cloud OpenFeign ###
1. [https://spring.io/projects/spring-cloud-openfeign](https://spring.io/projects/spring-cloud-openfeign)
2. It provides integrations for Spring Boot apps through autoconfiguration and binding to Spring Environment and other Spring programming model idioms (?).

### Spring Cloud Function ###
1. [http://github.com/spring-cloud/spring-cloud-function](http://github.com/spring-cloud/spring-cloud-function)
2. It promotes the implementation of business logic via **functions**.
3. It supports **uniform programming model across serverless poviders**
4. It supports the ability to run standalone (locally or in a PaaS)

### Release Trains ###
1. Spring Cloud is an umbrella project consisting of independent projects with in principle, different release cadences.
2. BOM (Bill of Materials) is published with a curated set of dependencies on individual project

## Learn ##
### Documentation ###
1. [2022.0.4 Refernce Doc](https://docs.spring.io/spring-cloud/docs/current/reference/html/)

### Get Started Guides ###

## Samples ##
### Config Server ###
### Service Registry ###
### Business Application ###
### OAuth2 Authorization Server ###
### OAuth2 SSO Client ###
### Integration Test Samples ###
### Spring Cloud Contract Samples ###

## Spring Cloud Config ##
1. It provides server and client-side support for externalized configuration in distributed system
2. Config server: It offers a central place to manage external properties for applications across all environments
3. They map to Spring `Environment` and `PropertySource`
4. Can be used with any application running in any language
5. As an application moves through deployment pipeline from dev to test to production, we can manage config between the environments and be certain that applications have everything they need to run when they migrate
6. Default implementation of server storage backend uses git.
    1. It supports labelled versions of config environment
    2. It makes it accessible to a wide range of tooling for managing content
    3. Easy to add alternative implementation and plug them in with Spring Config

### Features ###
1. Spring Cloud Config Server Features:
    1. HTTP based API for external config (name-value pairs, or equaivalent YAML content)
    2. Encrypt and decrypt property values (symmetric or asymmetric)
    3. Embeddable easily in a Spring Boot app
        1. Using `@EnableConfigServer` **(M)**
2. Config Client Features (for Spring applications)
    1. Bind to Config Server and initialize Spring `Environment` with remote property sources
    2. Encrypt and decrypt property values (symmetric or asymmetric)

### Getting Started ###
1. If Spring Boot Actuator & Spring Config Client are on classpath, a Spring Boot app will try to contact a config server on [http://localhost:8888](http://localhost:8888)
    1. It is the default value of `spring.cloud.config.uri` **(M)**
        1. It can be changed by setting `spring.cloud.config.uri` in `bootstrap.[yml | properties]` or via **system properties** or **environment variables**
2. Example:

        @Configuration
        @EnableAutoConfiguration
        @RestController
        public class Application {
            @Value("${config.name}")
            String name = "World";

            @RequestMapping("/")
            public String home() {
                return "Hello " + name;
            }

            public static void main(String[] args) {
                SpringApplication.run(Application.class, args);
            }
        }

    1. `config.name` - can come from local config or from **Config Server**
        1. Config Server takes precedence by default
    2. Go to `/env` endpoint and see `configServer` property sources
3. How to run my own server?
    1. Use `spring-cloud-config-server` **(M)** dependency
    2. Add `@EnableConfigServer` **(M)**
    3. If `spring.cofig.name=configserver` is set, then app will run on port 8888 and serve data from sample repository (git repo)
    4. Set `spring.cloud.config.server.git.uri` to locate configuration data for our own needs
        1. It is location of git repo by default
            1. It can be a local `file:..` URL

### Quick Start ###
1. Step 1: Start the server as follows:

        $ cd spring-cloud-config-server
        $ ../mvnw spring-boot:run