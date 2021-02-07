- offsetsは2つのニュアンスで言われている。
- > Committing offsets only after processing has completed for a given event or batch of events is a FaaS best practice. 
  - ここでのoffsetは、「offsetsをcommitする」。committing offsetsという名詞があるわけではない。
- > Triggering Based on Consumer Group Lag
  - [gkzz.md](./gkzz.md) で書いた、「ここでいう「オフセット」とは、Record番号のことであり、ConsumerがRecordをどこまで読みだしたのかを示す？」はこっち

- offsetするのは、processingしたあと

- warmするのに気にするほどチャージかからないのでは？
  - cf. [AWS Lambda で最長 15 分間実行に要する関数の取扱いが可能に](https://aws.amazon.com/jp/about-aws/whats-new/2018/10/aws-lambda-supports-functions-that-can-run-up-to-15-minutes)
  - re:inventで最長60分になったと告知された？

- buildpackのセッション
  - > コンテナのビルド周りのセッションを持つので、興味があるかたはご参加ください。前提知識はDockerfileを書けるぐらいを想定してます。

- lambdaはkinesisの件数によって起動できる

- Figure 9-4. Choreographed asynchronous function calls within a bounded context

- [Apache Spark™ - Unified Analytics Engine for Big Data](https://spark.apache.org/)
- [Apache Beam](https://beam.apache.org/)

- [Network Connectivity Center. Google Cloud に Network Connectivity… | by Seiji Ariga | google-cloud-jp | Feb, 2021 | Medium](https://medium.com/google-cloud-jp/network-connectivity-center-4205a057cc02)

- [Workflows  |  Google Cloud](https://cloud.google.com/workflows)

- [Airflow web interface  |  Cloud Composer  |  Google Cloud](https://cloud.google.com/composer/docs/how-to/accessing/airflow-web-interface)

- [Amazon Managed Workflows for Apache Airflow (MWAA) – Amazon Web Services](https://aws.amazon.com/managed-workflows-for-apache-airflow/)

- [Amazon Elasticsearch Service – Amazon Web Services](https://aws.amazon.com/elasticsearch-service/)

- [Apache ZooKeeper](https://zookeeper.apache.org/)

- **※読書会参加者のみなさまへ**
  - 現在扱っている「Building Event-Driven Microservices」も残り3回程度で完走するので、次の課題図書を決めていきます。
  - #recommended に本やplaylistのリンクなどぜひ！！
