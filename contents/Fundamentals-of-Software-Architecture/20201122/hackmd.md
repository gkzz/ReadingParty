# Fundamentals of Software Architecture Chap.6-8

- イベントページ
  - [READING.10 #技術書を英語で読む会](https://reading.connpass.com/event/195476/)
- 課題図書
  - [Fundamentals of Software Architecture: An Engineering Approach](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
- 貼っている画像の引用先
  - [Updated Fundamentals of Software Architecture Images](http://fundamentalsofsoftwarearchitecture.com/images.html)
- これまでのイベントで扱ったHackMDのリンク集
  - [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@gkzz/H1fdY9jOP)


### written by @gkzz 

- Chap.6
※本章を読み進めるにあたって、`“evolutionary” ` の理解に苦しめられたので、本章で取り上げられている[進化的アーキテクチャ ―絶え間ない変化を支える](https://learning.oreilly.com/library/view/untitled/9784873118567/)を読んで再挑戦したｗ
  - > They aren’t physics
    - システムの設計の特徴はコンテキストによって変わるというのは、モノの判別ほどくっきりできることはないということ？
      - 「〜性」とか場面場面で違う 
  - > Too composite
    - 開発しているシステム全体がまさにこれ。 一部の管理画面に対するリクエストに対してレスポンスを返すところがfatなところなど。
  - > Operational Measures
    - `外れ値の検知`って自前？SaaSにおまかせですか？（私がいるところは閾値を超えたら通知するだけ、外れ値検知は無かったような。）
      - 場面によって平均値、最大値をとればいいか変わる。最大値としても1台、10台走っているかでも変わる
  - > That guidance mechanism is called `a fitness function`: an object function used to assess how close the output comes to achieving the aim.
    - fitness function(適応度関数)はテストコードとの違いがよく分からなかったので調べた。
    - [読書メモの見返し(進化的アーキテクチャ第2章 適応度関数)](https://note.com/ryoma_0923/n/na019812888e9)より
      > 適応度関数を用いて定量・定性的な判断を行えるようにすることで`システムの非機能的な観点でのコミュニケーションの円滑化などを図る`
    - [米動画配信のNetflix、Chaos MonkeyのおかげでAmazon EC2のメンテナンスリブートを難なく乗り切る](https://www.publickey1.jp/blog/14/netflixchaos_monkeyamazon_ec2.html)より
      > Amazon EC2のインスタンスをランダムに落としまくることで、サービスに対して仮想的な障害を引き起こしてくれます。これにより、サービスがきちんと冗長化され、耐障害性を持つように作られているかどうかを日常的に検証できる

- Chap.7
なし

- Chap.8 
 ![](https://i.imgur.com/nb8D3KV.png =300x)
  - `Domain partitioning` v.s. `Technical partitioning`
  - > While there is no one true way to ascertain components, a common anti-pattern lurks: `the entity trap.`
  - > `this anti-pattern(entity trap)` generally indicates `lack of thought about the actual workflows of the application`. Components created with the entity trap also tend to be too `coarse-grained`, offering no guidance whatsoever to the development team in terms of the packaging and overall structuring of the source code. 
    - `coarse-grained`: adj
      - meaning: coarse in texture or grain, 目の粗い
        - e.g.: "coarse-grained soil"
  -  ![](https://i.imgur.com/HduNSit.png =300x)
  -  > the architect has basically taken each entity identified in the requirements and made a Manager component based on that entity. This isn’t an architecture; it’s an object-relational mapping (ORM) of a framework to a database.
    - ORM使っていようが、↓で言うようにMVC以外のところに業務ロジックを書いたほうが綺麗（テストが書きやすい）になっていいと思う。業務ではORM使って業務ロジックをがっつりview(DjangoではController)に書いていて感じた。
  - cf. [変更に強いアーキテクチャについてIT業界19年目の僕が超ザックリ説明する](https://qiita.com/lobin-z0x50/items/39131a4f47ed7c5df443)
    - `Fat Controller `対策としてのサービスモジュールの導入 
      - ![](https://i.imgur.com/g2AhUwJ.png =300x)
      - > Service モジュール内に、業務や機能の分類ごとにサービスクラスを作っていき、業務ロジックはすべてそこに追い出してしまう。Controller は単にサービスクラスを呼び出すだけ。で、サービスの出力を View に渡したり、処理結果（または例外キャッチ）を元に画面遷移したりという風に本来の Controller の仕事に専念すればよい。
  - `サービス`を作ったところでそれが肥大化したままでは意味なし。DDDやること。 
  - > `Event storming` as a component discovery technique comes from domain-driven design (DDD) and shares popularity with microservices, also `heavily influenced by DDD`. 


### written by @y-wat

- Chap.6 アーキテクチャ的諸特徴を測定し統治する
    - アーキテクチャ的諸特徴を測定する
    アーキテクチャ的諸特徴への客観的な定義により3つの問題を解決する
    アーキテクチャ的諸特徴への硬い定義を組織横断で合意する
    ユビキタス言語を構築する
    測定可能な特徴を明らかにするために複合的な特徴を解く
        - 操作的測定
        アーキテクチャ的特徴は直接的な指標を持っているが、それでもニュアンス的な解釈を必要とする。高度なチームによっては統計的な解析も行う。
        - 構造的測定
        アプリケーションのコーディング構造に対する評価。包括的なメトリックは無いが、いくつかのメトリックとツールは存在する。
        例えば循環的複雑度(cyclomatic complexity)。
        - プロセス測定
    - 統治と適合度関数
        - アーキテクチャ的諸特徴を統治する
        - 適合度関数
        目的に結果がどの程度迫っているかを測る客観関数(機能？)
        アーキテクチャの評価手法
        新しいものではなく、既存ツールの新しい見方
        メトリック、モニタリング、テスト、カオスエンジニアリングetc
            - 循環依存
            - distance from the main sequence fitness function
- Chap.7 scope of architecture characteristics
アーキテクトはコードの外にある依存コンポーネントを考慮する必要がある
アーキテクチャのquantum(訳が思いつかない)
    - coupling and connascence
    connascence: 片方へのある変化が他方への改修を必要とするのであれば両者はconnascentである
    static: コード分析で発見できる
    dynamic: 走行環境に依存する(synchronous/asynchronous)
    - architectural quanta and granularity
    機能的結合(funnctional cohesion): システムの意味的な結合
    architecture quantum: 高い機能的結合と同期的connascenceを持つ独立してデプロイ可能な物
    独立してデプロイ可能: 各々のarchitecture quantumは動作に必要なコンポーネントを自身に含んでいるということ。モノリスだとシステム全体で一つのarchitecture quantumになる。マイクロサービスではシステムに複数のarchitecture quantumが存在する。
    高い機能的結合: cohesionはコードが目的にどの程度統一化？(unified)されているかを反映する。高い機能的結合はarchitecture quantumが合目的であることを意味する。DDDのbounded contextに通じる。
    同期的connascence: arcitecture quantumを形成する同期的な呼び出し
    同期的呼び出し(=connascence)が動的connascenceを作り出すこともある
        - case study
        Bidder: Availability, Scalability, Performance
        Auctioneer: Availability, Reliability, Scalability, Elasticity, Performance
        Bidder: Reliability, Availability, Scalability, Elasticity
- Chap.8 コンポーネントを軸に考える
    - コンポーネントのスコープ
    コンポーネントで指すものはいくつか有る: コードをまとめたライブラリ、サブシステムやレイヤ、サービス
    コンポーネントはアーキテクチャの基礎的なモジュールを構成する
    - アーキテクトの役割
    アーキテクトはコンポーネントを定義し管理する
    コンポーネントはソフトウェア・システムでアーキテクトが関わる最下層(コードの品質指標は除く)
    個別クラス設計等の決定にアーキテクトがトップダウンで決定してはいけない
        - アーキテクチャのパーティショニング
        コンポーネントの定義はコンテナメカニズム(docker仮想化の話ではない)を反映するので、これもまたトレード・オフである
        トップレベルパーティショニング: レイヤードモノリスとモジュラモノリスの比較
        レイヤード: 技術的トップレベルパーティショニング、開発者に解りやすいのでデフォルトに採用されやすい。欠点としてレイヤーと人間組織が一致しがち(コンウェイの法則)。
        モジュラモノリス: ドメインパーティショニング。DDDの系譜。マイクロサービスもDDDの延長。
        根本的な違いはトップレベルパーティショニングに何を置くか。
        技術的な関心により分割: レイヤ間での依存が限定できる。しかし任意のドメイン機能は複数レイヤに跨る。特定ドメインの機能改修はレイヤ全体の改修に繋がる。
        - ケーススタディ
            - ドメインパーティショニング
                - 利点
                ビジネス機能にモデルが基づく
                機能横断チームを作るために逆コンウェイをきかせやすい
                モジュラモノリスやマイクロサービスと親和的
                分散アーキテクチャに移行可能
                - 欠点
                コードの改変が多くの場所に発生する(似たようなコードがあちこちに出現しがち)
            - 技術的パーティショニング
                - 利点
                改修コードを明確に分離する
                レイヤードアーキテクチャに近似する
                - 欠点
                一箇所への改修が全体に波及しやすい
                データとアプリケーションが密接に結合してしまう(他のアーキテクチャに移行しづらい)
    - 開発者の役割
    アーキテクトによるコンポーネント設計を決定版とみなしてはいけない
    ソフトウェアデザインはイテレーションで作り上げる
    - コンポーネントの識別フロー
        - 始まりのコンポーネントを識別する
        まずトップレベルパーティショニングの型に基づきトップレベルコンポーネントを定義する
        初期のコンポーネントから良いデザインを達成する度合いは低いので、アーキテクトはコンポーネントをイテレート的に向上させなければならない
        - コンポーネントに要求を割り当てる
        要求またはユーザストーリを割り当ててフィット具合を見る
        正確である必要はない(テックリードや開発者と話をすすめるための粗いもので良い)
        - 役割と責任を分析する
        役割と責任が要求の粒度と一致するか見る
        適切なコンポーネントの粒度を見極めるのは難しい
        - アーキテクチャ的特徴を分析する
        コンポーネントへの要求を割り当てたら、アーキテクチャ的特徴についてもコンポーネント分割への影響を見る必要がある
        - コンポーネントを再構築する
        イテレーションは付き物
    - コンポーネントの粒度
    細かすぎても粗すぎても不適切な結果になるので難しい
    - コンポーネントのデザイン
    正確な方法はないがテクニックは有る
        - コンポーネントを発見する
        目的は問題空間をアーキテクチャ的特徴の区分を考慮した粗い部分に分割する初期デザイン
            - エンティティの罠
            アーキテクチャの分割をORM的なエンティティ分割と混同すること
        - アクター/アクションアプローチ
        ユーザとシステムへの動作を明らかにする
        - イベントストーミング
        DDDに由来する考え方
        メッセージやイベントを軸にコンポーネント考える
        イベント駆動と相性が良い
        - ワークフローアプローチ
    - ケーススタディ
    - モノリスまたは分散アーキテクチャを選択する
    architecture quantumはアーキテクチャ的特徴のスコープを定義する -> アーキテクトはモノリスと分散の選択を迫られる
    モノリス: 単一デプロイのユニットであり、プロセスで走行するシステムのすべての機能が含まれており、単一のデータベースに接続されている
    分散: 複数の独立リリースサイクルを持つモジュールに分割される
    要求されるアーキテクチャ的特徴が分かれるのであれば分散アーキテクチャになる

### written by @fujiwara

- Chap.6
    - Structural Measures: CYCLOMATIC COMPLEXITY
        - 適切なしきい値は問題のドメインの複雑さに依存する。アルゴリズム的に複雑な問題がある場合など。
        - 問題のドメインまたは不十分なコーディングによって機能が複雑化しているか？あるいは、コードのパーティション化が不十分か？
            - 大きなメソッドをより小さな論理的なチャンクに分割し、作業（および複雑さ）をより適切に因数分解されたメソッドに分散可能か？
    - THE ORIGIN OF THE SIMIAN ARMY: Chaos Engineering
        - [Netflixのテックブログ](https://netflixtechblog.com/)はブログの都合上、良くお世話になっていますが、パフォーマンスチューニング、内製ツールのOSS化など、面白いものが多いです。
- Chap.8
    - Chapter.7も含めて言っている事は何となく理解できるが、頭に残らない。こういった課題感や観点が養われていないからだと思うので、キーワードを目の届くところに置いておいて深掘りして行きたい。自身の血肉になるように。
        - コンウェイの法則と、逆コンウェイの法則
        - テクニカルとドメインパーティショニング
        - コンポーネントの識別フロー、デザイン

### written by @hodagi

- Chap.6
    - ビルドツールであるBazelの良さについて、解説するブログを拝見して...
        - Bazelの良さはキャッシュを活用した高速性にある
        - それだけならmavenなど既存のパッケージ管理ツールでもできるけど、
            - 完全に隔離されたsandbox環境
            - 依存関係をバージョンも含めて全部最初に書かせる
            - 依存解決用のアルゴリズムがここに出てくるような話
        - を用いることでキャッシュしやすいステージ構造を作り出しているという話だった
    - ArchUnitは [マイクロサービスアーキテクチャをあきらめないための、モノリスで始めるアーキテクチャテスト](https://speakerdeck.com/kawanamiyuu/jjug-ccc-2020-fall?slide=46)で名前を知ったけど、趣旨はわかりやすかった
        - マイクロサービスと違ってモノリスの場合、IFで明示的に切っているわけではないからレイヤーを意識しないとすぐに技術負債を起こす
        - それを防ぎ、階層化レイヤーやオニオンレイヤーといった取り決めを守っているよねってチェックするのがArchUnitの目的。
    - SimianArmyリストラされてなかったっけ？
        - →[PROJECT STATUS: RETIRED](https://github.com/Netflix/SimianArmy)ですね。
        - →[Chaos Monkey](https://github.com/netflix/chaosmonkey)だけ、スタンドアローンのプロジェクトとして、Spinnakerと統合されて提供されているようです。(知らなかった)
    - Fitness Functions
        - Progressive Deliveryとか、Chaos EngineeringをCI/CDに組みこもうとか、最近はこの制約をデリバリー過程で繰り返しチェックできる仕組みがわりと熱い気がする
- Chap.7
    - ![](https://i.imgur.com/iUV73vB.png)
    - まさかの第五章の例がそのまま7章へ...    
- Chap.8
    - DDD...ドメインをどうやって分割するか
        - ![](https://i.imgur.com/Ve4ZYT9.png)
    - ドメイン駆動設計入門読んでやり直したいです...
    - サンドイッチさんの例とgoing going gone社の例、この図が最初に欲しかった...
        - 英語の要件定義からモデル起こしているようなものじゃん!!

### 雑談メモ

- [Working with the Chaos Monkey](https://www.google.com/amp/s/blog.codinghorror.com/working-with-the-chaos-monkey/amp/)
- [ARC203 Highly Available Architecture at Netflix - AWS re: Invent 2012](https://www.slideshare.net/AmazonWebServices/arc203-netflixha)