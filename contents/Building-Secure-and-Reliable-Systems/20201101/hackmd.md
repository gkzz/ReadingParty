# Building Secure & Reliable Systems Chap.7-10

- イベントページ
  - [READING.7 #技術書を英語で読む会](https://reading.connpass.com/event/192746/)
- [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@gkzz/H1fdY9jOP)
- [Building Secure &Reliable Systems](https://static.googleusercontent.com/media/landing.google.com/en//sre/static/pdf/Building_Secure_and_Reliable_Systems.pdf)


### written by @gkzz 

- Chap.7
  - セキュリティの在り様が変わったきっかけってありますか？
    - e.g. システムの設計の変化、社内ルールの厳格化、有識者の参入
  - サービスのフェーズが移行するときのセキュリティ対応はたいへんそう。。
    - サービス立ち上げにコンテナはいらなくて、モノリシックな構成を選び、コンテナへ移行するときのセキュリティ対応など
    - cf. [私も「個人開発・スタートアップの最強のアーキテクチャ」考えてみた。](https://twitter.com/xhiroga/status/1321969844904845312?s=20)
    - 元ネタは[個人開発・スタートアップで採用すべき最強のアーキテクチャを考えた](https://qiita.com/yuno_miyako/items/fad33456d9c32d8f4483)
- Chap.8
　　-　下記の記述のようなケースに遭遇したことはありますか？
    > Consider deploying load-shedding and throttling capabilities if your organization’s scale or risk aversion justifies investing in active automation for resilience.
- Chap.9
  - 「めったに起きない障害」を考慮した設計をすると、「その障害が起きないための設計」をするべきではないか？と言われるのでツライという意味ですかね？
    > Designing systems for recovery is considered an advanced topic, whose business value is proven `only when a system is out of its intended state`. But, given that we recommend operating systems use an error budget to maximize cost efficiency,28 we expect such systems to be in `an error state regularly`. 
  - いざというときの「バックドア」、「裏API」のようなものはありですか？ (ダメです)
  - cf. [The Die is Cast | Hardware Security is Not Assured.- ACM Queue](https://queue.acm.org/detail.cfm?id=3431245)
- Chap.10
  - [DDoS 攻撃を示唆して仮想通貨による送金を要求する脅迫行為 (DDoS 脅迫) について](https://www.jpcert.or.jp/newsflash/2020090701.html)
   > JPCERT/CC は、2020年8月以降、DDoS 攻撃を示唆して仮想通貨による送金を要求する脅迫行為に関する情報を複数確認しています。

### written by @y-wat
- chap.7
    - ```Keeping references to dependencies up to date is particularly important for open source projects```
わかる。
    - container / microservice / CICD / SRE <- この辺の一体運用感
    - 自主的な脆弱性診断ってやってます？
    - ライブラリバージョン等の脆弱性もSREが集中監視すべきなんかね
    - リスクの正確な見積もりとは
    - [国家によるバックドア設置が進みそうな事案について](https://japan.zdnet.com/article/35160775/)
        - 犯罪者捜査は別のレイヤー/手法で対処して頂きたいと思うのは私だけですかね？[漫画村の遮断](https://www.legacy-cloud.net/special_topic_categories/4/special_topics/46)と同じで、特定の面しか見ていない人の判断に思います。どういうトレードオフでこの判断になったのか気になる。
- chap.8
    -  感想思いつかなかったので後回し
- chap.9
    - リカバリのために仕込んでいる仕組みやアクティビティを各自披露しましょう(守秘義務に触れない範囲で
- chap.10
    - DoSの潜在ターゲットを担当してないので書きづらい

### written by @fujiwara
- chap.7
  - ```Embargoed Vulnerabilities```と```Zero-Day Vulnerability```の流れでGoogleのスケールでの情報戦やパッチが垣間見えて興味深かった。
  - OTPからsecurity keyへのロールアウト完了後の学びが原則論として理解しつつ、多くの組織では実践されてなさそう。```This experience provided several generally applicable lessons, relevant for building a culture of security and reliability (see Chapter 21):```
      - Make sure the solution you choose works for all users.
      - Make the change easy to learn and as effortless as possible.
      - Make the change self-service in order to minimize the burden on a central IT team.
      - Give the user tangible proof that the solution works and is in their best interest.
      - Make the feedback loop on policy noncompliance as fast as possible.
      - Track progress and determine how to address the long tail. 
  - 最近、ECSタスクのリタイアの通知を受けて、ECS FargateはLive Migrationしてくれると過信していたことに気付きました。あと、機械翻訳語の質の向上希望。Chrome翻訳を使うか、QAを入れて欲しい。
      - [タスクのリタイア](https://docs.aws.amazon.com/ja_jp/AmazonECS/latest/developerguide/task-retirement.html)
      - 以下のシナリオで、タスクのリタイアを予定できます。
          - AWS は、タスクをホストしている基盤のハードウェアで回復不可能な障害を検出します。
          - Fargate 起動タイプを使用し、セキュリティ脆弱性のあるプラットフォームバージョンで実行されているタスクでは、パッチが適用されたプラットフォームバージョンを使用して新しいタスクを起動して、タスクを置き換える必要があります。
- chap.9
  - `What Are We Recovering From?`で`Malicious Actions`の対象として、客観的に権限と知見のあるインサイダーがいる可能性を念頭に置いて明記しておくのは大事だと思う。Hope is not a strategy.
      - `Humans can also work against your systems deliberately. These people may be privileged and highly knowledgeable insiders with the intent to do harm.`
- chap.10
  - ISPでDDoS攻撃を検知して対応していたことを思い出す。

### writte n by @hodagi
- chap.7
    - コントロールプレーンとデータプレーンの分離って時系列的にはサービスメッシュより前にSoftware Defined NetworkやOpenStack界隈から来ている用語だけど、マイクロサービスって個別サービスに横串のガバナンスや共通機能を提供するときも便利だよね、的な再発見の結果なのかなーなんて思う
    - Kubernetes Patternの著者のBilgin IbryamさんはMecha Architectureっておっしゃってた(流行ってほしいw) ![Image](https://1.bp.blogspot.com/-MOISRRX01SA/Xs7wQzy8wWI/AAAAAAAAOWQ/AfMlKt7ked83hFwy-tygdmcGv-gYZHOWgCK4BGAsYHg/d/mecha-architecture.png)
- chap.8
    - GCのタイミングなど...
    - ![image](https://learning.oreilly.com/library/view/building-secure-and/9781492083115/assets/bsrs_0804.png)
    - ALIGNING PHYSICAL AND LOGICAL ARCHITECTURE
    - cert-manager=認証鍵の自動ローテーションを行うk8s ossって結構普及された印象
    - managed な bastionサービスが求められそう
        - https://www.hashicorp.com/blog/why-we-built-hashicorp-boundary
- chap.9
    - https://github.com/coreos/rpm-ostree
- chap.10
    - 感想無し


### 雑談メモ

- [Kubernetes Patterns](https://learning.oreilly.com/library/view/kubernetes-patterns/9781492050278/)
  > Book Description
  > The way developers design, build, and run software has changed significantly with the evolution of microservices and containers.

- [firecracker-microvm](https://github.com/firecracker-microvm/firecracker)
- [Multi-Runtime Microservices Architecture](https://www.infoq.com/articles/multi-runtime-microservice-architecture/)