# 「Building Event-Driven Microservices」の3,4章
2021/01/10(Sun) 09:00am-10:00am

## 読書会当日に話したいこと

### Chap.3
- スキーマ定義個別にやるとなるとめんどくさいのかな？
  - > Duplicating efforts across services to ensure a consistent view of implicitly defined data is nontrivial and best avoided completely.
  - スキーマ定義はやったほうがよい。
  - 一人運用からチーム運用になるとき、スキーマは定義されていたほうがよさそう。

- `Schema Definition Comments` で出てくる、イベントに関するcommentについて
  - commentも更新する手間が煩わしくない？
    - コメントないとツライ
  - コメントがほしくなるとして単位は必要そう
    - > For example, a datetime field’s comments could specify if the format is UTC, ISO, or Unix time.

- `type field` の追加はアンチパターンであることが「？」ってなった。`type field`の追加の目的はバリデーションであり、バリデーションはおこなうべきではないからアンチパターン？ 
  - > One common anti-pattern is adding a type field to an event definition, where different type values indicate specific subfeatures of the event.

### Chap.4
- Summaryの「組織の文化によって〜」というのは、サービスを管轄する部署間の連携と相互理解が肝だということ？
  - > The culture of the organization dictates how successful data liberation initiatives will be in moving toward an event-driven architecture.
    - > 組織の文化によって、イベント駆動型アーキテクチャへの移行においてデータ解放イニシアチブがどのように成功するかが決まります。
      Source: https://translate.google.com

---

## 読書メモ

### Chap.3
- `convey`
  -  verb
  - meaning: transport or carry to a place.

- `misinterpret`
  - veb
  - meaning: misunderstand, misconceive, misconstrue, misapprehend, mistake, misread, put a wrong 

- event is as follows
  - >  is a statement of fact
  - > when combined with all the other events in a system, provides a complete history of what has happened.

- `adhere`
  - verb
  - meaning: stick fast to (a surface or substance)


- explict schemas v.s. implicit schemas as data contracts

|explict schemas                         | implicit schemas                      |
|----------------------------------------|---------------------------------------|
| be capable of enforcing data contracts |                                       |
| event format is prospective consumers  | data contracts are susceptible        |
| give security and stability to both consumers and producers    |               |

- `arbitary`
  - adj
  - meaning: based on random choice or personal whim, rather than any reason or system.

- Two schema evolution rules are as follows
  - Backward vs. Forward Compatibility
    - ![Backward vs. Forward Compatibility | by Steven Heidel | Medium](https://miro.medium.com/max/1104/0*PxX6E7xfjI2K7ayV)

    Source: [Backward vs. Forward Compatibility | by Steven Heidel | Medium](https://stevenheidel.medium.com/backward-vs-forward-compatibility-9c03c3db15c9)

    |                                        |Backward |Forward       |
    |----------------------------------------|---------|--------------|
    |Services with a new schema              |Reader   |Writer        |


- `スキーマ`
  - > データの構造の記述で、そのフィールドやデータ型が含まれる。データがスキーマに従っているかどうかは、そのデータの生存期間中の様々な時点でチェックでき(略)、スキーマは時間とともに変化しうる
    [用語集 | データ指向アプリケーションデザイン ―信頼性、拡張性、保守性の高い分散システム設計の原理](https://learning.oreilly.com/library/view/untitled/9784873118703/glossary.xhtml)より

- `シリアライズ`
  - > オブジェクトを記憶装置上のバイト列に表現すること
- `デシリアライズ`
  - > 記憶装置からデータを読み込んで Java オブジェクトに復元すること
    [Java オブジェクトのシリアライズとデシリアライズ - Java の入出力 - Java の基本 - Java 入門](https://java.keicode.com/lang/io-object-serialize.php)


### Chap.4
- `data liberation`
  - > Data liberation is the practice of allowing users to view and export the data that you have about them
    Source: [What is Data Liberation? - Simplicable](https://simplicable.com/new/data-liberation)

  - > Data liberation enforces two primary features of event-driven architecture: `the single source of truth and the elimination of direct coupling between systems.` 

  - > This data needs to be liberated `from these legacy systems` to enable other areas of the organization to compose new, `decoupled products and services`.

  - Three patterns
    - Query-based, Log-based, Table-based

- `double duty`
  - noun
  - meaning: a twofold function or role.

- `spectrum`
  - noun
  - meaning: used to classify something in terms of its position on a scale between two extreme points.

- `emit`
  - verb
  - meaning: produce and discharge (something, especially gas or radiation).
    - Syn: discharge, release

- `disrupt`
  - verb
  - meaning: interrupt (an event, activity, or process) by causing a disturbance or problem.

- `interrupt`
  - verb
  - meaning: stop the continuous progress of (an activity or process)
    - > Based on these definitions, I would say that “disrupt” may represent a more serious (and sometimes even violent) form of discontinuity than “interrupt” does, although its first definition describes it as “interrupt.”
      Source: [What is the difference between interrupt and disrupt? - Quora](https://www.quora.com/What-is-the-difference-between-interrupt-and-disrupt)

