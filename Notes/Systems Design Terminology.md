---
tags: 
- systems
---

## **Systems Design Terminology

[[Systems Thinking]]   [[Systems]]   [[Systems Thinking]]

![[6476c4a76322030c4ec81a76d564f587_MD5.jpg]]

Below are the top 50 must-know system design interview terminologies that we will explain with definitions and working examples, along with additional resources for learning.

## 1\. Scalability

-   **Definition**: It is the ability of a system to support increased load by adding resources.
-   **Example**: Addition of more servers to handle the increase in web traffic.
-   **Learn More**: [What is Scalability and How to Achieve it?](https://www.geeksforgeeks.org/what-is-scalability-and-how-to-achieve-it-learn-system-design/)

## 2\. Load Balancer

-   **Definition**: Dividing the incoming network traffic among multiple servers so that no one server processes a large amount of load.
-   **Example**: Load balancing web traffic across multiple EC2 instances using the AWS Elastic Load Balancer(ELB) Service.
-   **Learn More**: [Understanding Load Balancer](https://www.f5.com/glossary/load-balancer)

## 3\. Microservices

-   **Definition:** It is an architectural pattern forcing the structuring of an application as a collection of loosely coupled services.
-   **Example:** Breaking down a monolithic application into independent services responsible for user management, processing payments, and sending notifications.
-   **Learn More**: [What are Microservices?](https://aws.amazon.com/microservices/)

## 4\. CAP Theorem

-   **Definition**: It states that at best, only two out of three guarantees can be gained in a distributed system: Consistency, Availability, and Partition Tolerance.
-   **Example**: When to Trade Off Consistency for Availability — And Vice Versa — in Distributed Database Design.
-   **Learn More**: [Understanding CAP Theorem](https://www.scylladb.com/glossary/cap-theorem/)

## 5\. Sharding

-   **Definition**: It involves breaking down a large database into smaller pieces called shards for better management.
-   **Example**: Sharding a user database based on geographic region.
-   **Learn More**: [Database Sharding Explained](https://aws.amazon.com/what-is/database-sharding/)

## 6\. Latency

-   **Definition**: This gets defined as the time that it takes for data to travel from point A to point B.
-   **Example**: Measuring the delay involved in message delivery through a chat application.
-   **Learn More**: [Latency explained!](https://www.cloudflare.com/learning/performance/glossary/what-is-latency/)

## 7\. Throughput

-   **Definition**: A measure of the quantity of data a system processes in some timeframe
-   **Example**: Requests processed by a web server in one second.
-   **Learn More**: [Throughput in Computer Networks](https://www.techtarget.com/searchnetworking/definition/throughput)

## 8\. Cache

-   **Definition**: Any hardware or software component that stores data to obviate future requests for the same data, serving It quickly.
-   **Example**: Implementing Redis caching for repeated database queries.
-   **Learn More**: [Caching Explained](https://aws.amazon.com/caching/)

## 9\. Content Delivery Network (CDN)

-   **Definition**: A server system, geographically dispersed, that shows Web content to a user based on the geographical location from which he is accessing.
-   **Example**: Using Cloudflare CDN for faster web page loading.
-   **Learn More**: [What is a CDN?](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/)

## 10\. REST API

-   **Definition**: a type of architectural style designed to build web services where data is accessed and manipulated using HTTP requests.
-   **Example**: Designing the Social Media API by REST(Representational State Transfer) principles.
-   **Learn More**: [REST API Tutorial](https://restfulapi.net/)

## 11\. GraphQL

-   **Definition**: It is a language designed to query data, so it is much more powerful, efficient, and flexible than REST.
-   **Example**: Using GraphQL to query user information in a single request.
-   **Learn More**: [GraphQL Introduction](https://www.digitalocean.com/community/tutorials/an-introduction-to-graphql)

## 12\. ACID

-   **Definition**: A set of properties ensuring reliable processing of database transactions. The properties are Atomicity, Consistency, Isolation, and Durability.
-   **Example**: Ensuring that a banking transaction has ACID properties prevents corrupted data.
-   **Learn More**: [ACID Properties in Databases](https://www.geeksforgeeks.org/acid-properties-in-dbms/)

## 13\. BASE

-   **Definition**: An alternate to ACID that emphasizes Availability and Partition tolerance over strict-Consistency. Basically Available, Soft state, Eventually consistent system.
-   **Example**: Design of a highly available, eventually consistent NoSQL database.
-   **Learn More**: [BASE vs ACID](https://aws.amazon.com/compare/the-difference-between-acid-and-base-database/)

## 14\. NoSQL

-   **Definition**: A type of database designed to promote storage and retrieval of data modelled in ways other than the tabular relationships used in relational databases.
-   **Example**: Using MongoDB for a document-based data store.
-   **Learn More**: [What is a NoSQL Database?](https://www.mongodb.com/resources/basics/databases/nosql-explained)

## 15\. SQL

-   **Definition:** It is the standard language used for storing, manipulating, and retrieving data in relational databases.
-   **Example:** Writing SQL queries to get data back from a relational database.
-   **Learn More**: [SQL Tutorial](https://www.geeksforgeeks.org/sql-tutorial/)

## 16\. Database Indexing

-   **Definition**: It is a data structure technique that allows quick searching and access to data from a database.
-   **Example**: Create indexing on the column of User ID for searching speed enhancement.
-   **Learn More**: [Database Indexing](https://www.codecademy.com/article/sql-indexes)

## 17\. Replication

-   **Definition**: A process of copying and maintaining database objects in a multitude of databases which make up a distributed database system.
-   **Example**: It involves allowing a database to be highly available across different geographical locations using replication.
-   **Learn More**: [Database Replication](https://www.geeksforgeeks.org/data-replication-in-dbms/)

## 18\. Failover

-   **Definition**: A backup operational mode in which system component functions are taken over by other system components in case of loss of a primary system component.
-   **Example**: Built-in automatic failovers to standby servers in the event of a server failure of your internet applications.
-   **Learn More**: [Failover Vs Disaster Recovery](https://macquariecloudservices.com/blog/failover-vs-disaster-recovery/)

## 19\. API Gateway

-   **Definition**: A server that sits at the front of an API, receiving API requests, applying throttling and security policies, and then forwarding them to back-end services.
-   **Example**: Using AWS API Gateway to manage APIs.
-   **Learn More**: [What is an API Gateway?](https://www.f5.com/glossary/api-gateway)

## 20\. Service Mesh

-   **Definition**: A dedicated infrastructure layer for facilitating service-to-service communications between microservices.
-   **Example**: Integrating [Istio](https://istio.io/latest/about/service-mesh/) as a service mesh for the management of microservice interactions.
-   **Learn More**: [Introduction to Service Mesh](https://aws.amazon.com/what-is/service-mesh/#:~:text=A%20service%20mesh%20is%20a,the%20performance%20of%20the%20services.)

## 21\. Serverless Computing

-   **Definition**: A Cloud computing implementation that “dynamically allows for the allotment of machine resources by the cloud provider”.
-   **Example**: Run backend code without any server provisioning at your end using AWS Lambda.
-   **Learn More**: [What is Serverless Computing?](https://www.cloudflare.com/learning/serverless/what-is-serverless/)

## 22\. Event-Driven Architecture

-   **Definition**: A software architecture paradigm encouraging the generation, detection, and consumption of, and the reaction to, events in general.
-   **Example**: Design a system with event communications between microservices using Apache Kafka.
-   **Learn More**: [Event-Driven Architecture](https://aws.amazon.com/event-driven-architecture/)

## 23\. Monolithic Architecture

-   **Definition**: A software architecture wherein all the elements are fitted into a single application and run as a single service.
-   **Example**: Old traditional enterprise applications built as a single, large unit.
-   **Learn More**: [Monolithic vs Microservices Architecture](https://www.atlassian.com/microservices/microservices-architecture/microservices-vs-monolith)

## 24\. Distributed Systems

-   **Definition**: A model wherein components located on networked computers communicate with each other and coordinate their actions by passing messages.
-   **Example**: Designing a distributed file system like Hadoop.
-   **Learn More**: [Introduction to Distributed Systems](https://www.geeksforgeeks.org/what-is-a-distributed-system/)

## 25\. Message Queue

-   **Definition**: This method allows asynchronous, service-to-service communication in both serverless and microservices architectures.
-   **Example**: Using RabbitMQ to queue messages between services.
-   **Learn More**: [Message Queues Explained](https://aws.amazon.com/message-queue/#:~:text=Message%20queues%20allow%20different%20parts,to%20send%20and%20receive%20messages.)

## 26\. Pub/Sub Model

-   **Definition:** A messaging pattern in which senders (publishers) publish messages so abstractly that any one of them can end up being accessed by recipients without the sender having to even know the identity of the destination receivers (subscribers).
-   **Example:** A notification system that uses Google Cloud Pub/Sub.
-   **Learn More**: [Pub/Sub Messaging](https://aws.amazon.com/what-is/pub-sub-messaging/)

## 27\. Data Partitioning

-   **Definition**: Division of a database into smaller, manageable parts.
-   **Example**: Partitioning a table in a database by date to allow super-fast query execution.
-   **Learn More**: [Database Partitioning](https://www.cockroachlabs.com/blog/what-is-data-partitioning-and-how-to-do-it-right/)

## 28\. Horizontal Scaling

-   **Definition**: Increasing the capacity by adding more machines or nodes within a system.
-   **Example**: Adding more web servers to handle an increasing volume of user traffic.
-   **Learn More**: [Horizontal vs Vertical Scaling](https://www.digitalocean.com/resources/article/horizontal-scaling-vs-vertical-scaling)

## 29\. Vertical Scaling

-   **Definition**: Upgrading an already existing machine with more power in the form of a CPU or RAM.
-   **Example**: Upgrading the RAM of a server so that it can handle more requests all at once.
-   **Learn More**: [Horizontal vs Vertical Scaling](https://www.digitalocean.com/resources/article/horizontal-scaling-vs-vertical-scaling)

## 30\. Rate Limiting

-   **Definition**: It means controlling the rate of traffic that the network interface controller is sending or receiving.
-   **Example**: Throttling an API to prevent abusive behaviour.
-   **Learn More**: [Understanding Rate Limiting](https://www.solo.io/topics/rate-limiting/)

## 31\. Circuit Breaker Pattern

-   **Definition**: A design pattern used in modern software development, applied to detect failures and encapsulate the logic of preventing a failure from constantly recurring.
-   **Example**: Handling failed remote service calls using a circuit breaker in a microservice architecture.
-   **Learn More**: [Circuit Breaker Pattern](https://www.geeksforgeeks.org/what-is-circuit-breaker-pattern-in-microservices/)

## 32\. Data Consistency

-   **Definition**: Ensuring that data is the same across multiple instances and is not corrupted.
-   **Example**: Maintaining the consistency of user data through multiple replicas of a database.
-   **Learn More**: [Data Consistency Models](https://www.geeksforgeeks.org/consistency-model-in-distributed-system/)

## 33\. Eventual Consistency

-   **Definition**: A model of consistency used in distributed computing toward the goal of high availability, stating that updates to a system will eventually propagate and be reflected by all nodes.
-   **Example**: Amazon DynamoDB provides an eventually consistent model for the read operation.
-   **Learn More**: [Eventual Consistency](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadConsistency.html)

## 34\. Strong Consistency

-   **Definition**: A consistency model ensuring every read gets the most recent write on a given unit of data.
-   **Example**: Using strong consistency in a financial transaction system.
-   **Learn More**: [Strong Consistency](https://www.geeksforgeeks.org/eventual-vs-strong-consistency-in-distributed-databases/)

## 35\. Containerization

-   **Definition**: Basically, this is whenever an application and its dependencies are encapsulated into a container to be run on any computational environment.
-   **Example**: Using Docker to containerize the applications for deployment in various environments such as dev, test, prod etc.
-   **Learn More**: [What is Containerization?](https://aws.amazon.com/what-is/containerization/)

## 36\. Kubernetes

-   **Definition:** An open-source platform that automates the process of application container deployment, scaling, and operation.
-   **Example:** Run and deploy containerized applications using Kubernetes.
-   **Learn More**: [Kubernetes Documentation](https://kubernetes.io/docs/home/)

## 37\. Autoscaling

-   **Definition**: Automatically adjusting the number of computational resources based on the user load.
-   **Example**: Utilizing AWS EC2 Auto Scaling feature to dynamically adjust the number of instances.
-   **Learn More**: [Auto Scaling explained](https://aws.amazon.com/autoscaling/)

## 38\. Multi-Tenancy

-   **Definition:** Architecture where a single instance of a software application serves multiple consumers/customers.
-   **Example:** SaaS applications, such as Salesforce, utilize multi-tenancy in their service provision toward their different categories of customers.
-   **Learn More:** [Single Tenancy Vs Multi-Tenancy?](https://www.digitalguardian.com/blog/saas-single-tenant-vs-multi-tenant-whats-difference)

## 39\. Load Shedding

-   **Definition**: Backing off some demands or degrading services to maintain the health of the overall system under high load.
-   **Example**: This will turn off all non-essential services during times of peak traffic.
-   **Learn More**: [Load Shedding](https://www.techtarget.com/searchdatacenter/definition/load-shedding)

## 40\. Idempotence

-   **Definition**: A property for some mathematical and computer-science operations stating that it has the same effect if repeated more times than once.
-   **Example**: An HTTP DELETE request is idempotent.
-   **Learn More**: [Idempotence in APIs](https://restfulapi.net/idempotent-rest-apis/)

## 41\. Quorum

-   **Definition**: The minimum number of votes needed to commit a distributed transaction.
-   **Example**: Basically, quorum-based replication ensures that consistency exists in the distributed database.
-   **Learn More**: [Quorum Systems](https://en.wikipedia.org/wiki/Quorum_(distributed_computing))

## 42\. Orchestration

-   **Definition**: A pattern of service interaction where a central coordinator controls the interaction between services.
-   **Example**: Using a workflow engine to manage some multi-step business process.
-   **Learn More**: [Orchestration](https://www.redhat.com/en/topics/automation/what-is-orchestration)

## 43\. Choreography

-   **Definition**: A service interaction pattern in which every service is self-contained and interacts with others through events; there will not be any coordinator or orchestrator.
-   **Example**: Microservices communicating through an event bus in a choreography pattern.
-   **Learn More**: [Choreography vs. Orchestration](https://www.wallarm.com/what/orchestration-vs-choreography#:~:text=With%20orchestration%2C%20the%20control%20logic,its%20part%20of%20the%20workflow.)

## 44\. Service Registry

-   **Definition**: A database that keeps track of instances of microservices.
-   **Example**: Using the Eureka service registry in a microservice architecture.
-   **Learn More**: [Service Registry and Discovery](https://docs.spring.io/spring-cloud-netflix/docs/current/reference/html/#spring-cloud-eureka-server)

## 45\. API Rate Limiting

-   **Definition**: It means controlling how many requests a client can make against an API within a certain timeframe.
-   **Example**: Limiting requests to an API to 100 per minute to prevent abuse.
-   **Learn More**: [API Rate Limiting](https://datadome.co/bot-management-protection/what-is-api-rate-limiting/#:~:text=API%20rate%20limiting%20is%2C%20in,API%20product's%20growth%20and%20scalability.)

## 46\. Data Warehouse

-   **Definition:** A system that helps in the generation of reports and business data analytics; the hub of Business Intelligence.
-   **Example:** Amazon Redshift can be implemented in data warehousing.
-   **Learn More**: [Understanding Data Warehouse?](https://aws.amazon.com/data-warehouse/)

## 47\. Data Lake

-   **Definition:** A system or repository where data is kept in native/raw format, generally as object blobs or files.
-   **Example:** Petabyte scaling for storing and managing structured and unstructured data in a data lake.
-   **Learn More**: [Data Lake](https://azure.microsoft.com/en-us/solutions/data-lake/)

## 48\. OLAP

-   **Definition:** Online Analytical Processing : The software category that allows the analysis of data kept in a database.
-   **Example:** Use of the OLAP cubes for pointy analytical and arbitrary queries.
-   **Learn More**: [OLAP Explained](https://aws.amazon.com/what-is/olap/#:~:text=Online%20analytical%20processing%20(OLAP)%20is,smart%20meters%2C%20and%20internal%20systems.)

## 49\. OLTP

-   **Definition**: Online Transaction Processing: a class of systems that manage transaction-oriented applications.
-   **Example**: Using OLTP systems for transaction data management, as in banking systems etc.
-   **Learn More**: [OLTP Explained](https://aws.amazon.com/rds/oltp/)

## 50\. Big Data

-   **Definition**: Large, complex data sets that cannot be efficiently managed by conventional data-processing software in the best of cases.
-   **Example**: Analyzing social media interactions to predict fashion trends.
-   **Learn More**: [Introduction to Big Data](https://www.geeksforgeeks.org/what-is-big-data/)

Keep in mind that it’s all about continuous learning and practice as you go further in system design. You can work with the resources, get involved in the discussions, and practice these concepts in your projects. The resources and discussions will expose you to the vocabulary and usages of the concept.

[[Systems]]