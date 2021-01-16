# 「Building Event-Driven Microservices」の5,6章
2021/01/17(Sun) 09:00am-10:30am

## 読書会当日に話したいこと

### Chap.5
- TransformationsのMapとMapValueについて。Mapを使うときはMapValueでは要件を満たせないときのみ？ValueだけではなくKeyを変えたくなるときってたとえばどういうとき？
  - > Note that if you change the key, you may need to repartition to ensure data locality.

- `data locality`について深堀した
  - そもそも`data locality`とは
    - > ローカリティ（locality）パフォーマンス最適化の一種で、頻繁に同時に必要になる複数のデータ片を同じ場所に置くこと。
     Source: [データ指向アプリケーションデザイン ―信頼性、拡張性、保守性の高い分散システム設計の原理](https://learning.oreilly.com/library/view/untitled/9784873118703/)
  - jsonやNoSQLはlocalityの考えが使われている
    - > JSONの表現であれば、すべての関連情報は1カ所に集まっているので、一度のクエリだけで十分
    - > リレーショナルの例でプロフィールをフェッチしようとすれば、複数のクエリを実行する

### Chap.6

- > The overarching goal of `deterministic processing` is that a microservice should produce the same output whether it is processing in real time or catching up to the present time.

同じってできるの？と疑問に感じたら、`best-effort determinism` と出てきて笑った。なかなか書籍でベストエフォートとか言わないよね？


---

## 読書メモ

### Chap.5
#### Basic idea
Event-driven microservices' process:
  - create a producer client and a consumer client
  - register itself with any necessary consumer groups
  - starts a loop to poll the consumer client for new events, processing them as they come in and emitting any required output events. 

- `traverse`
  - verb
  - meaning: move back and forth or sideways. 

Common transformations:
- Filter
  - > emits zero/one 
- Map
  - > Changes the key and/or value of the event, emitting exactly one event. 
  - > if you change the key, **`you may need to repartition to ensure data locality. `**
- MapValue
  - > Change **`only the value of the event, not the key. `** 
  - > **`Repartitioning will not be required.`** 
- Custom transforms
  - > Apply custom logic, look up state, and even communicate with other systems synchronously.


#### Necessities to branch event streams or to merge streams
- to branch event streams
  - to output it to **`a new stream based on the result`**
  - streamが増える

- to merge streams
  - to output to a single output stream
  - from multiple input streams are consumed
  -   streamが減る、以前あったものを結合する

See the details in Chap. 6
> how to handle consuming and processing events from multiple input streams in a consistent and reproducible order.

#### Repartitioning
- the act of producing a new event stream with one or more of the following properties:
  > - Different partition count
  > - Different event key
  > - Different event partitioner

- `delegate`
  - verb
  - meaning: entrust (a task or responsibility) to another person, typically one who is less senior than oneself. 
    - Syn: assign, entrust, give, pass on 

- `colocate`
  - verb
  - meaning: place side by side or in a particular relation.

### Chap.6
