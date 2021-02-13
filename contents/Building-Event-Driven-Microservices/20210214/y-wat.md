# Chapter 11. Heavyweight Framework Microservices
- お題: streaming frameworks
  - heavyweight
    - Spark, Flink, Storm, Heron, Beam
    - "it requires an independent cluster of processing resources to perform its operations"
    - "the leading Apache solutions traditionally rely on Apache Zookeeper, another clustered service, to provide high-availability support and coordinate cluster leader elections"
    - "the heavyweight framework uses its own internal mechanisms for handling failures, recovery, resource allocation, task distribution, data storage, communication, and coordination between processing instances and tasks"
  - lightweight

## A Brief History of Heavyweight Frameworks
- heavy weight batch-processing predecessors: Hadoop

## The Inner Working of Heavyweight Frameworks
- structure: cluster - master - worker
- workloads: ETL, session/window based analytics, detect abnormal patterns of behavior, aggregate streams and maintain state, perform any sort of stateless streaming operations
- shortcomeings:
 - not originally designed with microservice-style deployment
 - mostly JVM only
 - materializing an entity stream into an indefinitely retained table is not supported

## Cluster Setup Options and Execution Modes
- container management system: k8sにmaster機能を負担させる設計が出始めている

## Handling State and Using Checkpoints
- Checkpoints
  - snapshots of the application’s current internal state
  - are used to rebuild state after scaling or node failures
- states
 - oprator state: <partitionId, offset>
 - key state: <key, state>

## Scalinng Applications and Handling Event Stream Partitions

## Recovering from Failures

## Multitenancy Considerations

## Langugages and Syntax

## Choosing a Framework

## Example: Session Windowing of Clocks and Views

## 感想
- streaming processingの解説章だったな
- これevent driven microservices??
  - eventのstream処理であって、サービスではないような。
- "vm + zookeeper (+ yarn)"から"k8s + containner"に変わっていく予感

# Chapter 12. Lightweight Framework Microservices
- lightweight frameworks have no additional dedicated resource cluster for managing framework-specific resources
- Horizonal scaling, state management, and failure recovery are provided by the event broker and the CMS

## Benefits and Limitations
- benefit(?): Materialization of streams into tables, along with simple out-of-the-box join functionality, makes it easy to handle streams and the relational data that inevitably ends up in them
  - テーブルっぽい話出てきたっけ
- The lightweight model relies upon the event broker to provide the mechanisms for data locality and copartitioning through the use of internal event streams. The event broker also acts as the mechanism of durable storage for a microservice’s internal state via the use of changelogs, as discussed in “Recording State to a Changelog Event Stream”

## Lightweight Processing
- シャッフル処理はinternalなブローカーを介して行う

## Handling State and Using Changelogs
- The default mode of operation for lightweight frameworks is to use internal state backed by changelogs stored in the event broker

## Scaling Applications and Recovering from Failures
- change logを読み出して何やかんや
- hot relicaを用意してダウンタイム縮めたり

## Choosing a Lightweight Framework

## Languages and Syntax

## Stream-Table-Table Join: Enrichment Pattern

## Summary

## 感想
- lightweightのメリットがよくわからない
- 結局、kafka stream + kafka broker => kafkaなので, lightweightとheavyweightの違いがわからない