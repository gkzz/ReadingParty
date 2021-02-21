# 「Building Event-Driven Microservices」の13章
2021/02/21(Sun) 09:00am-10:30am

## 読書会当日に話したいこと
### Chapter 13. Integrating Event-Driven and Request-Response Microservices

* Autonomously Generated Events
* Reactively Generated Events
* Handling Autonomously Generated Analytical Events
* Integrating with Third-Party Request-Response APIs
* Processing and Serving Stateful Data


## 読書メモ

### Chapter 13. Integrating Event-Driven and Request-Response Microservices

* Autonomously Generated Events
* Reactively Generated Events
* Handling Autonomously Generated Analytical Events
* Integrating with Third-Party Request-Response APIs
* Processing and Serving Stateful Data
  * Serving Real-Time Requests with Internal State Stores
  * Hot replicas of state stores (see “Using hot replicas”) may also be used to serve direct-call requests, should your framework support their use.
  Keep in mind that hot-replica data may be stale in proportion to the replication lag from the primary state store.
  * One drawback of serving sharded internal state is that the larger the microservice instance count, the more spread out the state between individual instances. 
    * WARNING
    Using a smart load balancer is just a best effort to reduce latency.
    Due to race conditions and dynamic rebalancing of internal state stores, each microservice instance must still be able to redirect incorrectly forwarded requests.
  * Serving Real-Time Requests with External State Stores
    * CAUTION
    Ensure that state is accessed via the request-response API of the microservice and not through a direct coupling with the state store. Failure to do so introduces a shared data store, resulting in tight coupling between services, and makes changes difficult and risky.
  * SERVING REQUESTS VIA THE MATERIALIZING EVENT-DRIVEN MICROSERVICE
  * SERVING REQUESTS VIA A SEPARATE MICROSERVICE
    * NOTE
    While this pattern has two microservices operating on a single data store, there’s still just a single bounded context.
    These two microservices are treated as a single composite service.
    They reside within the same code repository and are tested, built, and deployed together.
    * One of the main advantages of this model is that because the request-response API is fully independent of the event processor, you can choose the implementation languages and scaling needs independently.
    * A second major advantage of this pattern is that it isolates any failures in the event processing logic from the request-response handling application.
    * The main disadvantages of this pattern are complexity and risk.
* Handling Requests Within an Event-Driven Workflow
  * Processing Events for User Interfaces
    * TIP
    Research and implement best practices for asynchronous UIs when handling user input as events. Proper UI design prepares the user to expect asynchronous results.
    * WARNING
    Intermittent network failures causing request retries can introduce duplicate events.
    Ensure that your consumers can handle duplicates idempotently, as covered in “Generating duplicate events”.
* Micro-Frontends in Request-Response Applications
  * The Benefits of Microfrontends
    * Microfrontend patterns match up very well with event-driven microservice backends, and inherit many of their advantages, such as modularity; separation of business concerns; autonomous teams; and deployment, language, and code-base independence.
  * Composition-Based Microservices
  * Easy Alignment to Business Requirements
* Drawbacks of Microfrontends
  * Potentially Inconsistent UI Elements and Styling
    * TIP
    Ensure common UI element libraries are free of any bounded-context-specific business logic.
    Keep all business logic encapsulated within its own proper bounded context.
  * Varying Microfrontend Performance
    * TIP
    The ability to materialize and consume any stream of business events, however the service needs them, is what makes event-driven microservice backends pair so effectively with microfrontends.
    


