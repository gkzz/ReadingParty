# 「Building Event-Driven Microservices」の14,15章
2021/02/28(Sun) 09:00am-10:30am

## 読書会当日に話したいこと
### Chapter 14. Supportive Tooling
なし。

### Chapter 15. Testing Event-Driven Microservices
- 基本的なテストの設計戦略は各サービスは疎結合とし、サービスが外部APIを使う場合はmockを使うことであるとすれば、Stateful Functionsのようなものを使ってテストするときは？テストケースに漏れがないようにどうするか？という気持ちで読み進めていた。
- そのなかでとりわけ、`Populating with events from production` などテスト環境を用意するにあたってデータを生成するやりかたの紹介、下記のGCPの記事がイチバンの学び。

#### Populating with events from production
- [DevOps 技術: テストデータの管理  |  Google Cloud](https://cloud.google.com/solutions/devops/devops-tech-test-data-management)
  - >  **`テストデータの管理に関する一般的な問題`** には、次のようなものがあります。
    - > テストでのデータへの過度の依存。特に、単体テストではテスト外部のデータや状態に依存しないようにしてください。
    - > テストに関連する部分や重要な部分を特定するのではなく、本番環境データベース全体のコピーを使用する。
    - > 機密データのマスキングやハッシュ化を行わない。
    - > 古いデータや関連性がなくなったデータに依存する。
  - > テストデータ管理の改善方法
    - > <img src="https://i.gyazo.com/4396e2c6e76faaa323f388553d4e8169.png" style="max-width:40%;">


---

## 読書メモ
### Chapter 14. Supportive Tooling
- > By following the single writer principle (see “Microservice Single Writer Principle”), you can attribute event stream ownership back to the microservice that owns the write permissions.
  - Chapter 2. has `Microservice Single Writer Principle`
  - Chapter 9.
    - > Triggering Based on Consumer Group Lag

#### One useful technique for assigning ownership
- > to tag streams with metadata
- Examples:
  -  Stream owner (service), Personally identifiable information (PII), Financial information, Namespace, `Deprecation`, Custom tags
  - Usecase of deprecation
    - > The new events can be put into the new stream, while the old stream is maintained until dependent microservices can be migrated over. Finally, the deprecated event stream owner can be notified when there are no more registered consumers of the deprecated stream, at which point it may be safely deleted. 

- Figure 14-1. Schema registry workflow for producing and consuming an event

#### Permissions and Access Control Lists for Event Streams
- WARNING
  - > you enable and enforce identification for your event broker and services as soon as possible, 
  - > Adding identification after the fact is extremely painful, as it requires updating and reviewing every single service that connects to the event broker. 

- Table 14-1. Typical event stream permissions for a given microservice

#### Cross-Cluster Event Data Replication
- > When selecting a replication tool implementation, consider the following:
  - > Does it replicate newly added event streams automatically?
  - > How does it handle the replication of deleted or modified event streams?
  - > Is the data replicated exactly, with the same offsets, partitions, and timestamps, or approximately?
  - > What is the latency in replication? Is it acceptable to the business needs?
  - > What are the performance characteristics? Can it scale according to business needs?

----
- `dearth`
  -  noun
  - meaning:  lack, scarcity, scarceness, shortage, shortfall, want, deficiency, insufficiency, inadequac
y

- `deprecation`
  - noun
  - meaning: In several fields, deprecation is the discouragement of use of some terminology, feature, design, or practice, typically because it has been superseded or is no longer considered efficient or safe, without completely removing it or prohibiting its use. 
    - Source: [Deprecation - Wikipedia](https://en.wikipedia.org/wiki/Deprecation)  

- `quota`
  - noun
  - meaning: a fixed share of something that a person or group is entitled to receive or is bound to contribute.
    - Syn: allocation  

- `hysteresis`
  - noun
  - > Hysteresis is the dependence of the state of a system on its history. For example, a magnet may have more than one possible magnetic moment in a given magnetic field, depending on how the field changed in the past. 
  - Source: [Hysteresis - Wikipedia](https://en.wikipedia.org/wiki/Hysteresis)

---
- [GCP: Operations (Stackdriver, Logging, Monitoring) - Qiita](https://qiita.com/ieiringoo/items/372bc4f21d1b19a10341)

---

### Chapter 15. Testing Event-Driven Microservices
- A great thing of testing event-driven microservices is they are very modular.

#### General Testing Principles
- > Event-driven microservices share the testing best practices that are common to all applications. 
- > Functional testing, such as unit, integration, system, and regression testing, 

#### Stateful Functions
- >  Stateful unit testing also requires that persistent state, whether in the form of a mocked external data store or a temporary internal data store, is available for the duration of the test.

-   Mocking the endpoint is one way of providing a reliable implementation of the data store for the duration of the test. Another option is creating a locally available version of the data store, though this is more akin to integration testing, which will be covered in more detail shortly. 

#### The topology testing frameworks
- time-based aggregations, event scheduling, and stateful functions perform as expected.
- > What data do you need to determine success or failure? Is manually crafted event data sufficient? Programmatically created? Does it need to be real production data? If so, how much?

#### How to prepare remote testing environment
- By populating with events from production
  - 上記で引用した[DevOps 技術: テストデータの管理  |  Google Cloud](https://cloud.google.com/solutions/devops/devops-tech-test-data-management)の方法
- By populating with events from a curated testing source
- By creating mock events using schemas
- By testing using a shared environment
- Testing using the production environment

#### Summay
- > The tradeoff is the increased difficulty in managing the event data, ensuring validity, and clarifying ownership.

---
- `populate data`
  - > to populate a database means to add data to it.
    - Source: [What is meant by populating database? - Quora](https://www.quora.com/What-is-meant-by-populating-database)

---
- [MrPowers/spark-fast-tests: Apache Spark testing helpers (dependency free & works with Scalatest, uTest, and MUnit)](https://github.com/MrPowers/spark-fast-tests)
- [TopologyTestDriver (kafka 2.4.1 API)](https://kafka.apache.org/24/javadoc/org/apache/kafka/streams/TopologyTestDriver.html)
- [Kafka Streams DSLを一通り体験する(1. 準備編) - Qiita](https://qiita.com/aaaanwz/items/d17ae435f6cff14d243c)