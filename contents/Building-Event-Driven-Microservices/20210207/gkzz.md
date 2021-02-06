# 「Building Event-Driven Microservices」の7,8章
2021/01/31(Sun) 09:00am-10:30am

## 読書会当日に話したいこと

### Chap. 9 Microservices Using Function-as-a-Service

- ここでいう「オフセット」とは、Record番号のことであり、ConsumerがRecordをどこまで読みだしたのかを示す？
  - > Committing offsets only after processing has completed for a given event or batch of events is a FaaS best practice. It is important for you to understand how offsets for your specific function-based solutions are handled, so let’s take a look at the implications of each approach.

  - cf: [Apache KafkaのProducer/Broker/Consumerのしくみと設定一覧 - Qiita](https://qiita.com/sigmalist/items/3b512e2ab49b07271665)
    - > Consumerはアプリケーションの再起動時に、自身のOffsetから再開できるようOffsetを永続化する必要があります。そのため、Consumerは自身のOffsetをKafka上のOffset用Topicや、任意のデータストアに保存します。

---

## 読書メモ

### Chap. 9 Microservices Using Function-as-a-Service

#### 再利用のしすぎは要注意
> An often-cited feature of FaaS frameworks is that they make it easy to write a single function and reuse it in multiple services. 

#### ひとつのFaaSサービス（lambdaひとつ）にひとつの機能を
> FaaS solutions may incorporate multiple functions to solve the business requirements of the bounded context, and while this is not an uncommon or bad practice, a good rule of thumb for FaaS solutions is that fewer functions are better than many granular functions. Testing, debugging, and managing just one function is much easier than doing the same for multiple functions.
 
#### Cold Start and Warm Starts
- [サーバーレスアンチパターン今昔物語 - YouTube](https://www.youtube.com/watch?v=pLl9jwXQUro&feature=youtu.be)
- [#serverless_newworld 2020-07-09 - HackMD](https://hackmd.io/@wo9kArhySpqHB8xOPPpYRQ/rkM4CtV1P)
- [LambdaのProvisioned Concurrencyを使って、コールドスタート対策をしてみた #reinvent | Developers.IO](https://dev.classmethod.jp/articles/lambda-provisioned-concurrency-coldstart/)
- [安い？それとも高い？Provisioned Concurrencyを有効化したLambdaのコストに関する考察 #reinvent | Developers.IO](https://dev.classmethod.jp/articles/simulate-provisioned-concurrency-cost/)

#### currently do not support triggering directly from open source brokers.ということは？？？
- > FaaS solutions from Google, Microsoft, and Amazon provide this trigger for usage with their proprietary event brokers, but currently do not support triggering directly from open source brokers. 

- Figure 9-1. Integrated event-stream listener with FaaS framework
- Figure 9-2. External event-stream listener application provided by Kafka Connect
  - [openfaas/faas: OpenFaaS - Serverless Functions Made Simple](https://github.com/openfaas/faas) 

#### Triggering Based on Consumer Group Lag
- [14. Supportive Tooling - Building Event-Driven Microservices](https://learning.oreilly.com/library/view/building-event-driven-microservices/9781492057888/ch14.html#ch_tooling_lag_monitoring) 

#### Triggering 
- Based on Consumer Group Lag
- on a Schedule
- Using Webhooks
- on Resource Events

---

- `albeit`
  - conjunction
   - meaning: though.
     - e.g.: "he was making progress, albeit rather slowly"

- `comprise`
  - verb
  - meaning: consist of; be made up of.
    - Syn: contian, take in
 
- ` granularity`
  - noun
  - meaning: the scale or level of detail in a set of data. 

- `blur`
  - verb
  - meaning: make or become unclear or less distinct.
    - e.g.: "tears blurred her vision"
    - Syn: unfocus, soften, obscure, dim 

- `a rule of thub`
  - meaning: A rule of thumb is a guideline, idea, or principle that helps you make decisions. 
    -  e.g.: "Arrive early" is a good rule of thumb for most appointments.  

### Chap. 10 Basic Producer and Consumer Microservices
#### Basic producer and consumer (BPC) microservices 
-  usecases are simple patterns such as stateless transformations
  - > External state stores are more commonly used

- sidecar pattern
  - >  to add new functionality to a system without requiring significant changes to the legacy codebase.
  - cf. [Sidecar pattern - Cloud Design Patterns | Microsoft Docs](https://docs.microsoft.com/en-us/azure/architecture/patterns/sidecar)
    - <img src="https://gyazo.com/06b69d0913535f6828d7ca9c08136d65.png" style="max-width:40%;">
  -  cf. [コンテナ・デザイン・パターンの論文要約　 - Qiita](https://qiita.com/MahoTakara/items/03fc0afe29379026c1f3)
  - cf. [コンテナのデザインパターンを学べる論文「Design patterns for container-based distributed systems」を読んだ - kakakakakku blog](https://kakakakakku.hatenablog.com/entry/2018/09/24/003723)

- >  The BPC is also a suitable approach when the underlying data layer performs most of the business logic, such as a geospatial data store; free-text search; and machine learning, AI, and neural network applications
