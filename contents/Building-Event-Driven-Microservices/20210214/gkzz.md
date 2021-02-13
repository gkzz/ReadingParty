# 「Building Event-Driven Microservices」の11,12章
2021/02/14(Sun) 09:00am-10:30am

## 読書会当日に話したいこと

### Chap. 11 Heavyweight Framework Microservices

- Google Dataflowすごそう。。
- GCP Dataflow類似サービス
  - [Amazon Kinesis vs Google Cloud Dataflow | What are the differences?](https://stackshare.io/stackups/amazon-kinesis-vs-google-cloud-dataflow)より
    - > Amazon Kinesis and Google Cloud Dataflow can be categorized as "Real-time Data Processing" tools.
    - > **`Amazon Kinesis has a broader approval, being mentioned in 130 company stacks & 24 developers stacks;`** compared to Google Cloud Dataflow, which is listed in 32 company stacks and 8 developer stacks.
    - Amazon Kinesis's user: Lyft, Zillow
    - Google Cloud Dataflow: Spotify, Resultados Digitais, Kapten. 


### Chap. 12 Lightweight Framework Microservices
なし

---

## 読書メモ

### Chap. 11 Heavyweight Framework Microservices

- This chapter covers
  - aspects of Apache Spark, Apache Flink, Apache Storm, Apache Heron, and the Apache Beam model

#### Some defining characteristics of a heavyweight streaming framework
- 1st
   - requires an independent cluster of processing resources to perform its operations.
- 2nd
  - uses **`its own internal mechanisms for handling failures, recovery, resource allocation, task distribution, data storage, communication, and coordination`** between processing instances and tasks. 

#### A Brief History of Heavyweight Frameworks
- MapReduce -> Storm/Heron or Spark/Flink
- MapReduce
  - was powerful, it executes slowly in comparison to many of today’s options. 
  - As these data sets have grown so has the demand for faster processing, more powerful options, simpler execution options, and solutions that can provide near-real-time stream-processing capabilities.

#### Figure 11-1. A generic view of a heavyweight stream-processing framework
- > Zookeeper provides highly reliable distributed coordination and is used to determine which master node is in charge (as it is not uncommon for nodes to fail, be they workers, masters, or  Zookeeper nodes). Upon failure of a master node, Zookeeper helps decide which of the remaining masters is the new leader to ensure continuity of operations. 

#### The heavyweight frameworks' usecases
- Extract data, transform it, and load it into a new data store (ETL)
- Perform session- and window-based analysis
- Detect abnormal patterns of behaviorAggregate streams and maintain state
- Perform any sort of stateless streaming operations

#### The heavyweight frameworks' shortcomings
- not originally designed with microservice-style deployment in mind
- most of these frameworks are JVM (Java Virtual Machine)-based, which limits the implementation languages you can use to create singular microservice applications. 
- materializing an entity stream into an indefinitely retained table is not supported out of the box by all frameworks.

#### Figure 11-3. Single job deployed on and managed by Kubernetes cluster


#### How to overcome the potential risks of internal staets
-  the potential risks of internal staets
   - carry some risks, such as state loss due to disk failure, node failures, and temporary state outages due to aggressive scaling by the CMS.
 - How to overcome them
   - use of checkpoints, which are snapshots of the application’s current internal state, and are used to rebuild state after scaling or node failures. 

#### Google Dataflow
- > Google Dataflow, which executes applications written with the Beam API, provides built-in scaling of both resources and worker instances. Heron provides a (currently experimental) Health Manager that can make a topology dynamic and self-regulating. This feature is still under development but is meant to enable real-time, stateful scaling of topologies.

#### Autscaling Applications
- > Some frameworks may have autoscaling options built in, such as Google’s Dataflow engine, Heron’s Health Manager, and Spark Streaming’s dynamic allocation functionality.
-  14章に書いてあり
  - > Others may require you to collect your own performance and resource utilization metrics and wire them up to the scaling mechanism of your framework, such as the lag monitor tooling discussed in “Consumer Offset Lag Monitoring”.
   
---
#### 単語帳(順不同)

- `aforementioned`
  - adj
  - meaning: mentioned earlier: 

- `shortcoming`
  - adj
  - meaning: a fault or failure to meet a certain standard, typically in a person's character, a plan, or a system.
     - Syn: defect, fault, flaw, imperfection, deficiency, limitation, blemish

- `preclude`
  -  verb
  - meaning: prevent from happening; make impossible.
    - Syn: prevent 

- `dedicate v.s. devote`
  - > Dedicate is usually found in cases where you are "dedicating" a physical object to something, while devote is found when one "devotes" an abstract concept to something else.
  - source: [What is the difference between "dedicate" and "devote" ? "dedicate" vs "devote" ? | HiNative](https://hinative.com/en-US/questions/140033) 

---
- [zookeeper とは - Qiita](https://qiita.com/szit/items/aec0ce677a28c83c6893)
- [Consul vs. ZooKeeper, doozerd, etcd | Consul by HashiCorp](https://www.consul.io/docs/intro/vs/zookeeper)
- [How to Write a Better Scribe - Dropbox](https://dropbox.tech/infrastructure/how-to-write-a-better-scribe)
  - 2015年ですが、Dropboxがzookeeperを採用したというお話
    - > How Can We Make Scribe Better?
    - > Problem:
    - > whenever configuration changes, we need to restart nodes to pick up the changes.  While this approach works well for tens, maybe even hundreds, of nodes, this approach is unsustainable for tens of thousands of nodes.
    - > Solution: NewScribe solves these issues by storing the configurations in zookeeper.  Whenever configurations change in zookeeper, NewScribe will pick up the changes and reconfigure itself automatically (without restarting).
 - [Deploying a pipeline  |  Cloud Dataflow  |  Google Cloud](https://cloud.google.com/dataflow/docs/guides/deploying-a-pipeline) 
   - > The Dataflow service fully manages Google Cloud services such as Compute Engine and Cloud Storage to run your Dataflow job, automatically spinning up and tearing down the necessary resources. The Dataflow service provides visibility into your job through tools like the Dataflow Monitoring Interface and the Dataflow Command-line Interface. 
 - [Google Cloud Dataflow がデータ分析基盤に使われる理由](https://www.dsk-cloud.com/blog/what-is-google-cloud-dataflow) 
   - > 動作環境構築が不要
   - > 各種GCPサービスと連携した処理が可能  


### Chap. 12 Lightweight Framework Microservices

#### Benefits
- applications can be dynamically scaled as they are under execution. 
- There is no need to restart an application just to change parallelism, though there may be a delay in processing due to consumer group rebalancing and rematerialization of state from the changelog. 

#### Considerations of scaling a lightweight application
- Event Shuffling
- State Assignment
- State Replication and Hot Replicas

#### Frameworks
- Apache Kafka Streams
- Apache Samza: Embedded Mode