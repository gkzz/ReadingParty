# Chap.1-2


## Chap.1
  - mediumの変遷が人対人の関係性、社会構造に変化をもたらしたように、`computer system architectures`もまた人対人との関係性に変化をもたらした
    - > each new medium has fundamentally changed people’s relationship with computing
    - > The medium of the asynchronously produced and consumed event has been fundamentally shifted by modern technology
  - > Microservices and microservice-style architectures have existed for many years, in many different forms, under many different names.
    - cf. https://fukabori.fm/episode/29 の「集中と分散の螺旋」
    - Service-oriented architectures
      - be composed of multiple microservices
      - communicate synchronously
    - Message-passing architectures
      - communicate asynchronously
    - **`Event-based communication`**
      - not new
      - `It's new to handling big data sets, at scale and in real time`
      - > these services can be stateful or stateless, complex or simple; and they might be implemented as long-running, standalone applications or executed as a function using Functions-as-a-Service
  - > **`Domain-driven design`**, (略), introduces some of **`the necessary concepts for building event-driven microservices`** 
  - > **`more specialized skill sets can be provided on a cross-team, as-needed basis`**. These best practices are covered in more detail in **`Chapter 14`**
    - Chap.14. Supportive Tooling 
  - event driven microservicesの有用性について
    - Communication Structures in Traditional Computing
      -　> This model encourages many direct point-to-point couplings, which become problematic to maintain as an organization grows 
    - Event-Driven Communication Structures
      - not replacement for request-response communications
      - Chap.3 has details
    - benefits of using event-driven microservices
      - **`granularity/scalability/flexibility on tech and biz requirements/loosely coupling/CD support/high testability`**

  - 単語帳
    - > Each of these inventions 
        - `invention` (noun) <- `invent` (verb)
          - meaning: create or design (something that has not existed before); be the originator of.
          - Syn: originate, create, innovate
    - > These events can now be persisted indefinitely 
      - `persist` (verb)
        - meaning: continue to exist; be prolonged.
        - Syn: continue, hold, carry on
    - > These improvements to the humble and simple event-driven medium have far-reaching impacts
      - `humble`
        - meaning: having or showing a modest or low estimate of one's importance.
        - Syn: meek, deferential, respectful
      - > `far-reaching`
        - meaning: having a wide range or effect  
    - > The internal operations of the context should be intensive and closely related
      - `intensive`
        - meaning: concentrated on a single subject or into a short time; very thorough or vigorous.
        - Syn: thorough, in-depth, concentrated
    - > Bounded contexts should be highly cohesive
      - cf.[Difference Between Cohesion and Coupling](https://stackoverflow.com/questions/3085285/difference-between-cohesion-and-coupling)
        - > Good software design has high cohesion and low coupling. 
        - > Cohesion is the indication of the relationship within a module
        - > Coupling is the indication of the relationships between modules
        - <img src="https://i.imgur.com/RYfnrEg.png" style="max-width:40%;">
    - > Conversely, aligning microservices on technical requirements is problematic
      - `problematic` (adj)
        - meaning: constituting or presenting a problem. 

    - > laborious to obtain via point-to-point connections
      - `laborious` (adj)
        - meaning: requiring considerable time and effort.
        - Syn: arduous, hard, heavy

  - よく分からなかったこと
    - `Leveraging Domain Models and Bounded Contexts` の **`Leverage`** とは、subdomainを分割しすぎて。 **`ideally a bounded context and a subdomain will be in complete alignment`** ができなくならないように。という意味が込められている？
      - > This division process repeats **`until the subdomain models are granular and actionable and can be translated into small and independent services by the implementing teams. `**`
    - microservicesはDDDのように望ましい設計条件はある？
      - |DDD/bounded contexts | microservices |
        |---------------------|---------------|
        |be built around business requirements and not technological requirements | aligning microservices on technical requirements is problematic | 
      - どこかの章でヒントがあるかも
        - > These tradeoffs will be examined in greater detail throughout this book
    - `If you find that it is too hard to access data in your organization` で始まるCAUTIONで出てくる **`you’re likely experiencing the effects of poor data communication structures`** とはたとえばどういった構造はpoor？
      - 直前で書かれている、`Databases may provide read-only replicas; however, this can expose their inner data models unnecessarily.` のことを指している？


  - 雑多メモ
    - [Confused about Bounded Contexts and SubDomains](https://stackoverflow.com/questions/18625576/confused-about-bounded-contexts-and-subdomains)


## Chap.2
  - producer microservices v.s. consumer microservices 
    |producer                        |consumer                        |
    |--------------------------------|--------------------------------|
    |produce events to event streams |consume from input event streams|
    - the stateless(Chap.5) / the stateful(Chap.7) / the sync- req-res APIs(Chap.13)
  - > Communication between event-driven microservices is completely asynchronous.
  - **`the table-stream duality`**
    - > you can convert a table into a stream of entity events by publishing each update to the event stream
    - > fundamental to the creation of state in an event-driven microservice
  - event brokers v.s. message brokers
    - |event brokers |message brokers |
      |--------------|----------------|
      |retains them for as long as the organization needs |deletes events after acknowledgment

  - **`The microservice tax`**
    - includes the cost of managing, deploying, and operating the event broker, CMS, deployment pipelines, monitoring solutions, and logging services.
    - `paid by the organization or by each microservices`

  - 単語帳
    - > A microservice topology details the inner workings of a single microservice. A business topology, on the other hand, details the relationships between services. 
      - `topology` (noun)
        - meaning: the way in which constituent parts are interrelated or arranged
        - cf. [Difference between network diagram and network topology?](https://superuser.com/questions/832773/difference-between-network-diagram-and-network-topology)
          - > A Network Topology is the actual design of a network. A Network Diagram is a diagram (drawing) of a network.
        - > be often used to mean the processing logic of an individual microservice.
        - > be used to refer to the graph-like relationship between individual microservices, event streams, and request-response APIs.
    - > The microservice topology ingests events from event stream A
      - `ingest` (verb)
        - meaning: jjjjabsorb (information), take in or soak up (energy or a liquid or other substance) by chemical or physical action.
    - > an arbitrary grouping of services
      - `arbitary`
        - meaning: based on random choice `or personal whim`, rather than any reason or system.
        - Syn: capricious, whimsical, random

 - 雑多メモ
   -  [イベントドリブンなマイクロサービスアーキテクチャ](https://yunkt.hatenablog.com/entry/2018/10/14/234311)
   -  [LINEの大規模データパイプラインを支える、Apache Kafkaプラットフォームの運用の裏側](https://logmi.jp/tech/articles/320330)  



