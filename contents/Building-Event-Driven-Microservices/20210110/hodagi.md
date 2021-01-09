# Chapter3

## 読書メモ
* この章の主軸は、サービスの修正、変更によりスキーマが変わっていったときに  
  送り手(producer)と受け取り手(consumer)でその差分をどうやって吸収するか？  
    * ![](https://learning.oreilly.com/library/view/building-event-driven-microservices/9781492057888/assets/bedm_0302.png)
    * スキーマの変更を伴うようなABテストはきつそう。
        * 最初にスキーマの部分だけこっそり入れておいて、画面は別途変更する？
        * この修正意味ないねってわかったら捨てデータ扱いかな...

* Event Design
    * Tell the Truth, the Whole Truth, and Nothing but the Truth
    * Use a Singular Event Definition per Stream
    * Use the Narrowest Data Types
    * Keep Events Single-Purpose

* Event DesignのBad Case
    * Avoid Events as Semaphores or Signals  
      (セマフォまたはシグナルとしてのEventは避ける)
        * ダメなのか..
        * Event完了時に、リソースの場所と一緒に情報を送りたくなるが...

# Chapter4
* 既存システムをどうやってEvent Driven Architectureにリファクタリングするか？  
  あるいは、共存させるか
  * Data Liberation Patterns
    * Databaseへの書き込み、読み込みをEventに変換することでDataをLiberation(解放)する
    * [Data liberation pattern using the Debezium engine](https://i8c.be/2020/05/data-liberation-pattern-using-the-debezium-engine/)
        * DebeziumはRed Hatが主として開発しているOSS
        * DBへのデータ書き込みを元にEventを発行する(CDC, Change Data Capture)
            * 要はOracleのTrigger
    * ![](https://learning.oreilly.com/library/view/building-event-driven-microservices/9781492057888/assets/bedm_0406.png)
    * [CDCと既存の仕組みとの違い](https://www.hvr-software.com/blog/change-data-capture/)
        * DATE_MODIFIED
        * DIFF(Dataの比較)
        * Trigger
        * LogBase
* [Sync MySQL to PostgreSQL Using Debezium and KafkaConnect](https://medium.com/swlh/sync-mysql-to-postgresql-using-debezium-and-kafkaconnect-d6612489fd64)
  * データベースの移行作業でも使える？
