# Chapter 3. Communication and Data Contracts

## Event-Driven Data Contracts
メッセージのフォーマット決めと管理で頭が痛い、という話は前にも出ましたね<br>
`In the event-driven ecosystem, the event is the message and the fundamental unit of communication. An event must describe as accurately as possible what happened and why. It is a statement of fact and, when combined with all the other events in a system, provides a complete history of what has happened.`<br>
システム的には何を持ってイベントとするのか。
### Using Explicit Schemas as Coontracts
- data contractをどうやって定義するか。
  - what: data definition
  - why: triggering logic
- 明示的にスキーマ定義を利用した処理を実装するか、暗黙的に行うか
- consumerが勝手な読み方をするのはスキーマ定義とは別の話だと思われるので賛同しない

### Schema Definition COmments
- 説明書きは必要ですね。サンプルデータを書いておいてほしい。

### Full-Featured Schema Evolution
- スキーマバージョン情報を下流まで伝播させようとすると、スキーマストアを用意するしか思いつかないんだよな
 
#### Forward compatibility
#### Backward compatibility
#### Full compatibility

### Code Generator Support
- わかりますよ。しかし型含め安定運用させようとするとprotobufかto_json/from_jsonに頼るしか無いんだよな。

### Breaking Schema Changes

#### Accommodating breaking schema changes for entities
- 後続のビジネスロジックが崩壊するようなのは別問題として、それ以外はやはりprotobufでスキーマを伝播させるか、jsonで簡易に行くかの2通りなんだよな。たぶん。と思ったらこの手法は出てきてない。なぜ。
- 同一時期に複数スキーマが混在するのはあまりやりたくない。まあレコード自体にスキーマ情報を書き込んで読み出し側自身に使うスキーマを教える、とかでも不可能ではないが。
- event全作り直しは無いんじゃないかなぁ。下流も全部走行し直すの？

#### Accommodating breaking schema changes for events
- かならずevent stereamを分けろとおっしゃる。なぜ。
- イベントメッセージにパージ期限を付けてあるから、何なのか。

## Selecting and Event Format

### Tell the Truth, the Whole Truth, and Nothing but the Truth
- はい

### Use a Singular Event Definition per Stream
- はい

### User the Narrowest Data Types
- はい

### Keep Ebents Single-Purpose
- entityとして別だけどフィールドが似ているものをtypeで区別しようとするなと言う話ね

### Example: Overloading Event Definitions
- はい

### Minimize the Size of Events
- はい

### Involve Prospective Consumers in the Event Design
- これ同意できない。マイクロサービスである以上はイベントソーシングの前後は互いを知らないはずなので、破壊的変更がない限り上流は下流に所定の時点で変更を通知するだけでよく、下流も必要なときは上流にイベントの変更依頼をコミュニケーションする、で十分なはず。なぜ普段から上流の開発に下流が入らないといけないのか。

### Avoid Events as Semaphores or Signals
- 例えばバッチジョブの完了シグナルではなく、バッチ処理結果自体をメッセージに載せろと？数ＧBの機械学習モデルとかも？

## Summary

## 感想
- イベントにはスキーマ定義が必要。どこかに集約して保管するのも必要。しかし疎結合にしなければならない。むう。
- 論点は理解するが、解決方法はあまり賛同できず。みなさんどうしてるのかね。
- protobufあたりでメッセージのフォーマット管理を行うのが限界じゃないですかね。ただしインフラはk8sにしてprotobuf定義はサイドカー経由で定期配信する、みたいな運用にすることになる。

---
# Chapter4. Integrating Event-Driven Architectures with Existing Systems
- event streamsの導入はdata liberationの導入なんだと。
- eventの出力と蓄積についての章

## What is Data Liberation?
- cross-domainなデータの出力と統合戦略なんだと。
- single source of truthとシステム間の密結合除去が特徴なんだと。

### Compromises for Data Liberation
- `A stream of liberated events must materialize back into an exact replica of the source table` は? 書き戻す??
- `Any shared state should be published to the event broker first and materialized back to any services that need to materialize the state, including the service that produced the data in the first place` おおんまじか
- `the fundamental goal is to keep the internal data set synchronized with the external event stream through strictly controlled publishing of event data` データストアに先に書くパターン。世のCDC系。

### Converting Liberated Data to Events
- Liberatedされたデータもschematizedされる必要がある。はい。

## Data Liberation Patterns
- query, log, table
- timestampは必須。そうね。

## Data Liberation Frameworks
- `One of the most common anti-patterns is the exposure of internal data models to external systems, further increasing coupling instead of decreasing it, as is one of the major benefits of event-driven architectures` schematizationしてる時点で密結合っぽくはなってると思うけどな

## Liberating Data by Query
- 前のロードに時間がかかりすぎると次が走り始めて事故る。わかる。
- queryでpullするって良いイメージ無い。

### Bulk Loading

### Incremental Timestamp Loading

### Autoincrementing ID Loading

### Custom Querying

### Incremental Updating

### Benefits of Query-Based Updating

### Drawbacks of Query-Based Updating

## Liberating Data Using Change-Data Capture Logs
- cdcパターン広まってほしいな。そしてembulkとairflowは撲滅されてほしい。

### Benefits of Using Data Store Logs

### Draw back of Using Data Base Logs

## Liberating Data Using Outbox Tables
- eventを出力用の表に貯めると。

### Performance COnsiderations

### Isolating Internal Data Models
- sourceのデータ構造を露出させるのを著者が嫌う理由って何だろうね。
- RDBの正規化が下流の要求するフォーマットと合わない、みたいに書いてあるけど、そもそも下流が何をフォーマットや項目として欲しがるかなんて上流には判らないし、それを想定してeventを作れ、というのは密結合では。
  - 例えば席予約イベントだとして、席予約イベントのデータは席番号のみ?予約者情報は?店舗は?予約の付帯入力があった場合は?予約者の流入径路情報は?「席予約」情報の境界はどこ??有り得るパターンごとにすべての非正規化データを作れと??

### Ensuring Schema Compatibility

### Benefits of Event-Production with Outbox Tables

### Drawbacks of Event Production with Outbox Tables

### Capturing Change-Data Using Triggers
- トリガーにビジネスロジックってDDD派が最も嫌う実装だと思うのだが。

### Benefits of Using Triggers

### Drawbacks of Using Triggers

## Making Data Definition Changes to Data Sets Under Capture
- `This incompatibility will cause breaking schema changes that will impact all downstream consumers of the event stream` それを心配するならsource側にdata contract整合性の責任を担保させるべきではないと思う
- ということでテーブルはレコードの変更記録をそのままpublishするべきと思う

### Handling After-the-Fact Data Definition Changes for the Query and CDC Log Patterns

### Handling Data Definition Changes for Change-Data Table Capture Patterns

## Sinking Event Data to Data Stores

## The Impacts of Sinking and Sourcing on a Business
- data liberationチームと言うかデータエンジニアチーム必要になるよね
- しかし疎結合(チーム的にもシステム的にも)を維持しようとすると、source側でeventスキーマ強制は無理だと思う
- 各サービスをロバストに、と言いつつevent sourcingが中央で信頼性を握るってどうなの

## Summary

## 感想
- そもそもここでのイベント(とイベントが持つsingle source of truth)のスコープはどこだろう。事業(=ドメイン)?事業群?基幹系とか社内システムを含めた全社??
- eventってのはそれなりに絞り込んでフォーマットも元データとも変えるんだな。あまり良い方法とは思えないのだが。
- event streamがsingle source of truthなら、個々のエッジサービスが参照しているデータベースは何?? truthともnot truthとも判断つかないものを参照しているということになる??
- eventとして出力していない、しかし元システムでは利用するデータは何??嘘データ??
- serializationのcontractを行うストアやシステムのドメインがどこなのかで物議を醸さないか。sourceとは独立した別ドメインと考えたいが、そうすると別ドメインのアプリケーションコードが各々のsourceシステム中に紛れ込み、しかもトランザクションの成否を決めると。どうなんだそれ。
- どうしてもsource側でschima検証を行いたいなら、別途protobufに定義したものをアプリデプロイまたは起動処理の中でテスト処理走らせる、が限界ではないか。アプリをクラッシュさせるレベルのDB変更が再デプロイなしに走るとも思えないので、これで事足りるような。
- 個人的にはRDBの場合はCDC, no-sqlの場合はsaveするobjectをjsonifyしたものをそのままメッセージとして全量流して、どうするかはevent sourcingからpollingする側に任せるべきだと思うんですけどね。システムで発生したデータはすべてtruthだと思っているので、集約先的なsingle sourceはあっても場所的なsingle sourceってどうなのと思っている。そもそもほかが障害があっても自身は独立して動き続ける、というのが疎結合のそもそもの目的だと思うので、外部にtruthの問い合わせ先があって、そこと連動できないと稼働できないというのはどうなんだ。