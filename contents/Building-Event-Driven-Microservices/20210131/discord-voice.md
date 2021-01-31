- materialized
  - メモリ上に実体化、のせる
  - Figure 7-4. Global materialized state and nonglobal materialized state
  - Figure 5-2. Repartitioning an event stream

- 著者のイベントストリームの考えはFIFO
  - 本書のパーティションとは、kinesisのシャード。RDBの世界のパーティションとは違う。
  - cf. [Amazon Kinesis StreamsのリシャーディングがAPI一発で行えるようになりました](https://dev.classmethod.jp/articles/scale-your-amazon-kinesis-stream-capacity-with-updateshardcount/)

- [Why we moved from Apache Kafka to Apache Pulsar](https://streamnative.io/en/blog/tech/2020-04-21-from-apache-kafka-to-apache-pulsar)
  - > Pulsar was built to store events forever, rather than streaming them between systems. Furthermore, Pulsar was built at Yahoo! for teams building a wide variety of products across the globe. It natively supports geo-distribution and multi-tenancy. Performing complex deployments, such as keeping dedicated servers for certain tenants, becomes easy. We leverage these features wherever we can. This allowed us to hand off a significant portion of our custom logic into Pulsar.

- kafka神ｗｗｗ

- Figure 8-3. Simple orchestrated event-driven workflow
  - ここでのkafkaはパイプ以外にも求められる
  - cf. [apache spark - Is it recommended to use Kafka as a source of truth? - Stack Overflow](https://stackoverflow.com/questions/42495124/is-it-recommended-to-use-kafka-as-a-source-of-truth)
    - > EDIT: One problem I do see is that the constraints imposed by Cassandra are different from those imposed by Kafka. `Since Kafka imposes no constraints and will accept any data,` it might give the application a false sense of successful transaction by writing to Kafka. The same data might not succeed in Cassandra due to some constraint violation in Cassandra. Example constraint failure from Cassandra
  
  - データ置き場としてのS3と何が違う？

- [CloudNative Days Spring 2021 ONLINE](https://event.cloudnativedays.jp/cndo2021)

- [Serverless - connpass](https://serverless.connpass.com/)

- [AWSがDocker Hubの代替サービスを発表予告。パブリックにコンテナイメージを公開可能で50GBまで無料、AWSからなら何度でもプルし放題に － Publickey](https://www.publickey1.jp/blog/20/awsdocker_hub50gbaws.html)
  - > AWSのブログ「Advice for customers dealing with Docker Hub rate limits, and a Coming Soon announcement」（Docker Hubの利用制限にかかわるユーザーへのアドバイスと発表予告）で、この新コンテナレジストリサービスは次のように説明されています。
  - > 略
  - > AWSは数週間以内に、デベロッパーがコンテナイメージを公開し、共有し、デプロイできる新しいパブリックコンテナレジストリを提供予定です。この新しいレジストリにより、デベロッパーはコンテナイメージを保存、管理、共有、デプロイすることができ、誰もがコンテナイメージを発見しダウンロードできるようになります。

- 観測上では数年前からパブリック設定はあったはずなんですけどねぇ (´・ω・｀)
  - [Container Registry  |  Google Cloud](https://cloud.google.com/container-registry?hl=ja)
