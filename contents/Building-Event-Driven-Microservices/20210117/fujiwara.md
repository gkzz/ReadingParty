## 読書メモ

# Chapter5
- Branching and Merging Streams

# Chapter6
- timestamps
  - AWSのAMIの差分調査をした時に、/etc/chrony.confのrtcsyncの設定の有無で釈然としなかった。リアルタイムクロックが 11 分ごとに更新される設定。
    - EKS optimized AMIあり。ECS optimized AMI無し。
  - 時刻同期の性能比較しているFacebookのEngineeringブログ「[Building a more accurate time service at Facebook scale](https://engineering.fb.com/2020/03/18/production-engineering/ntp-service/)」は以前読んで面白かった。
- event scheduling
  - WARNING: Your microservice will need event scheduling if the order in which events are consumed and processed matters to the business logic.
- watermarks
  - A watermark is a declaration to downstream nodes within the same processing topology that all events of time t and prior have been processed. The node receiving the watermark can then update its own internal event time and propagate its own watermark downstream to its dependent topology nodes. 
- stream times
  - Apache Kafka Streamsで好まれる。