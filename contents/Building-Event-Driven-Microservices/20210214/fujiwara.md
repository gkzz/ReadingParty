## 読書メモ

### Chap. 11 Heavyweight Framework Microservices

- A second defining characteristic is that the heavyweight framework uses its own internal mechanisms for handling failures, recovery, resource allocation, task distribution, data storage, communication, and coordination between processing instances and tasks. This is in contrast to the lightweight framework, FaaS, and BPC implementations that rely heavily on the container management system (CMS) and the event broker for these functions.

- TIP
  - Some heavyweight frameworks are moving toward lightweight-like execution modes. These lightweight modes integrate well with the CMS used to operate other microservice implementations.
- A Brief History of Heavyweight Frameworks
  - Heavyweight stream-processing frameworks are directly descended from their heavyweight batch-processing predecessors. One of the most widely known, Apache Hadoop, was released in 2006, providing open source big-data technologies for anyone to use.
  - A job is a stream-processing topology that is built using the framework’s software  development kit (SDK) and designed to solve problems of the particular bounded context. It runs on the cluster indefinitely, processing events as they arrive, just like any other microservice described in this book.
- Benefits and Limitations
  - The heavyweight frameworks discussed in this chapter are predominantly analytical technologies. They provide significant value around analyzing large volumes of events in near–real time to enable quicker decision making.
  - First, these heavyweight frameworks were not originally designed with microservice-style deployment in mind.
  - Second, most of these frameworks are JVM (Java Virtual Machine)-based, which limits the implementation languages you can use to create singular microservice applications.
  - Third, materializing an entity stream into an indefinitely retained table is not supported out of the box by all frameworks. 
- Cluster Setup Options and Execution Modes
  - Use a Hosted Service
  - Build Your Own Full Cluster
  - Create Clusters with CMS Integration
  - DEPLOYING AND RUNNING THE CLUSTER USING THE CMS
  - SPECIFYING RESOURCES FOR A SINGLE JOB USING THE CMS
- Application Submission Modes
  - Driver Mode
    - Driver mode is supported by Spark and Flink. The driver is simply a single, local, standalone application that helps coordinate and execute the application, though the application itself is still executed within the cluster resources. 
  - Cluster Mode
    - Cluster mode is supported by Spark and Flink and is the default mode of deployment for Storm and Heron jobs.

### Chap. 12 Lightweight Framework Microservices

- Benefits and Limitations
  - The event broker also acts as the mechanism of durable storage for a microservice’s internal state via the use of changelogs, as discussed in “Recording State to a Changelog Event Stream”. 
    →筆者の頭の中では、やはりそこをdurable storageにするしかない？
- Scaling Applications and Recovering from Failures
  - Event Shuffling
  - State Assignment
  - State Replication and Hot Replicas
- Choosing a Lightweight Framework
  - Apache Kafka Streams
  - Apache Samza: Embedded Mode