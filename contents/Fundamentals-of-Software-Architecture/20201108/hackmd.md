# Fundamentals of Software Architecture Preface, Chap.2

- イベントページ
  - [READING.8 #技術書を英語で読む会](https://reading.connpass.com/event/194144/)
- 課題図書
  - [Fundamentals of Software Architecture: An Engineering Approach](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
- 貼っている画像の引用先
  - [Updated Fundamentals of Software Architecture Images](http://fundamentalsofsoftwarearchitecture.com/images.html)
- これまでのイベントで扱ったHackMDのリンク集
  - [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@readingparty/BJCW7wBTD)

### written by @gkzz 

- Preface
- Chap.1
  - ARBなるものを初めて知った
    - cf.[効果的なアーキテクチャレビューボードを構築する](https://hub.appirio.jp/tech-blog/architecture-review-board)
      > 要するに、ARBは社内で現在実装中の機能を見える化するための効果的な方法となりうるのです。
    - 以下は、自分にとって新しく学ぶ技術との付き合い方を示唆してくれる記述。「手になじんだ技術を増やす、類似する技術のメリデリを知る」と理解。
      > One of the best ways of mastering this expectation is for the architect `to stretch their comfort zone`.  it is far more valuable (略) and the associated `pros and cons` of each rather than to be an expert in only one of them.
      - アーキテクトとしての`Technical breadth`を強調していたので、手になじむまで行かなくても、詳細は分からないけれどもプロダクトとそれに関するメリデメリットを知り、ユースケースに応じて検討/提案ができる状態をイメージした。
          > `Technical breadth includes the stuff you know about, but not at a detailed level, combined with the stuff you know a lot about.`
  - SOAとMicroservicesの考え方の違いを調べた
    - cf.[「マイクロサービス」のメリットをざっくり言うと「変化に対応しやすい」こと](https://knowledge.sakura.ad.jp/3377/)によると、「複雑さ」
    - SOAの考え方が使われた当時はXML。現在の主流であるRESTful Web APIより複雑な仕様
    - Webサービスによりシステムコンポーネント間を結ぶためには、ESB（エンタープライズサービスバス）と呼ぶ複雑な（高価な）ミドルウェアが必要だったとのこと。
- Part I.
なし
- Chapter 2
　-　`Balancing Architecture and Hands-On Coding`で紹介されている`to do frequent proof-of-concepts or POCs. `に関わるという記述は、今後の自分のキャリアを考えるヒントとなりそう。 

### written by @fujiwara
- Preface
    - `Expectations of an Architect`
        - `Have business domain knowledge`
           課題感として大きい。SIで入っていると線を引いていたり、その関連のミーティングや、メーリスなどに入ってない場合が多々あり得る。アンテナを張ると共に、適宜認識合わせや合意が必要。
          >Without business domain knowledge, it is difficult to understand the business problem, goals, and requirements, making it difficult to design an effective architecture to meet the requirements of the business. 
        - `Possess interpersonal skills`
           「技術的に解決したい問題も漏れなく人の問題が付いてくる」と実感していたので、納得。
          >As technologists, developers and architects like to solve technical problems, not people problems. However, as Gerald Weinberg was famous for saying, “no matter what they tell you, it’s always a people problem.”
        - `Understand and navigate politics`
          正にこれ。相手の要望に沿うか、目的を達成できるか、その目的自体が問題解決につながっているのか、を常にヒアリング/検証しながら進めていく必要がある。依頼者/アーキテクトがミーティング時点でゴールが見えていない場合もあり、複数の選択肢を並べた上で要件に応じたその時点でのベストを出していく必要がある。そして、その決断の観点/根拠/プロセスをドキュメントとして残す必要あり。
          >The main point is that almost every decision an architect makes will be challenged. Architectural decisions will be challenged by product owners, project managers, and business stakeholders due to increased costs or increased effort (time) involved. Architectural decisions will also be challenged by developers who feel their approach is better. 

- Chap.2
    - Stuff you know → Stuff you must maintain
    - 唯一の専門性よりも、特定の問題を解決し得る5つの解決策の存在を知っている方が重要。
        - A large part of the value of an architect is a broad understanding of technology and how to use it to solve particular problems. For example, as an architect, it is more beneficial to know that five solutions exist for a particular problem than to have singular expertise in only one. 
    - 器用貧乏と賞味期限切れの専門性
        - an architect tries to maintain expertise in a wide variety of areas, succeeding in none of them and working themselves ragged in the process./ stale expertise
            - Frozen Caveman Anti-Pattern
                - While risk assessment is important, it should be realistic as well. 
    - Architecture is the stuff you can’t Google.
    - business drivers
 

### written by @y-wat
- Chap.1 Introduction
software architectのパスが何故無いのか?
1.良い定義がない
2.スコープが大きく、かつ広がり続けている
3.対象の移り変わりが速い
4.ソフトウェアアーキテクチャに関するマテリアルは概して「歴史的（時代背景依存）」な関連しか持たない
アーキテクチャは状況依存的なものとしてしか理解できない。状況による産物である。
    - Defining Software Architecture
ソフトウェアアーキテクチャを考える4軸
1.構造
2.アーキテクチャ的な諸特徴
3.アーキテクチャの諸決定
4.デザイン諸原則
構造: システムが実装されるアーキテクチャ形式のタイプ(マイクロサービス、レイヤード、マイクロカーネルetc)
アーキテクチャ的な諸特徴: システムの成功基準を定義する(ex: 可用性、信頼性、テスト可能性、スケーラビリティ、セキュリティ、アジリティ、耐障害性、エラスティック、復旧可能性、パフォーマンス、デプロイ可能性、学習可能性) <- 非機能要件に近いか?
アーキテクチャの諸決定: システムがどのように構築されるべきかのルール(レイヤ間でのアクセスルールとか)。複数システムに影響が出る決定は組織のアーキテクチャレビュー委員会またはチーフアーキテクトが判断する。
デザイン諸原則: ガイドラインでありルールではない。開発者が適切な手法を選ぶガイドになるもの。マイクロサービス間ではパフォーマンスのために非同期通信を採用しましょう、とか。
    - Expectations of an Architect
        - Make Architecture Decisions
        技術的な決定をチームが行うためのガイドとなるアーキテクチャの決定を行う。ガイドを決定するのであって、個別フレームワークの選定等を行うのではない。個別アーキテクチャ的特徴を保持するために細部に入ることも有る。
        - Continually Analyze the Architecture
        昔構築したシステムが今どの程度存続可能なアーキテクチャであるかをビジネスと技術の両面から評価し続けること。アジリティのためにテストとリリース環境を維持し続けることも忘れない。
        - Keep Current with Latest Trends
        知識は日々最新化しましょう。アーキテクトが行う決定は長く影響を持ち、変更も難しい。
        - Ensure Compliance with Decisions
        アーキテクトの決定に開発チームが従っている状態を維持する。
        - Diverse Exposure and Experience
        様々なテクノロジを広く知ること。コンフォートゾーンを広げていくこと。
        - Have Bussiness Domain Knowledge
        ビジネス課題を解決するアーキテクチャを建てるにはドメイン知識が必要。
        - Possess Interpersonal Skills
        人間関係スキルは重要。チームワーク、リーダーシップ、ファシリテーション。
        - Understand and Navigate Politics
        アーキテクトの決定は組織を横断する影響を持つ事がある。そういうときは交渉も必要になる。
    - Interssection of Architecture and... (交差領域)
        - Engineering Practices
        ソフトウェア開発プロセスとエンジニアリングの実践は区別すべき。
        プロセス: 人々を組織しインタラクトさせる機構
        エンジニアリングプラクティス: プロセス不可知論的な実践。Unknown unknowns. 決まったトラックをなぞる類の活動ではない、ということかな。
        アーキテクチャとエンジニアの実践は共生的な複雑な機構である（マイクロサービスを選択すると自動プロビジョニングや自動テストが想定される、みたいな）。
        進化的アーキテクチャが最新の形式。アーキテクチャ的な適合関数(?)を構築する。客観的な統合アセスメントの構築。これをアーキテクチャの評価に用いる。
        - Operations/DevOps
        運用は外注されてきた。しかし今日の運用におけるエラスティックスケーリングはアーキテクトの関心対象である。
        - Process
        アーキテクチャもイテレーティブな活動になってきている。アーキテクチャもどのようなプロセスでチームが運営されるかの影響を受ける。
        - Data
        ソフトウエアはいろいろな外部データベースに依存します。アーキテクトはデータレイヤを無視してはいけない。
    - Laws of Software Architecture
    アーキテクチャはトレードオフとの戦いである。whyを常に考えること。

- Chap.2 Architectural Thinking -- アーキテクチャ的な考え
アーキテクチャについて考えるよりも広い
アーキテクチャ的に考え、アーキテクチャ的に見る
    - Architecture Versus Design
    アーキテクトの関心: アーキテクチャ的な関心（xx性）、アーキテクチャパターンやスタイル、コンポーネント構造
    開発者の関心: クラス設計、UI、コード
    アーキテクトから開発者へ一方的な関係では開発側で成功しなかったりフィードバックが無い
    メンタリングやコーチングができる環境を築きましょう
    - Technical Breadth
    技術的な深さと技術的な横幅
    知っている要素、知らないと知っている要素、知らないことを知らない要素
    知っている要素: エキスパートであることが期待される領域。ここの大きさが深さ。
    アーキテクトの価値は幅広い技術理解と、問題解決のための利用法の知識。知らないと知っている領域もアーキテクトにとっては重要。
    幅広い全てのエキスパートであろうとしたり、古い知識のままエキスパートと思い込んではいけない
    - Analyzing Trade-Offs
    アーキテクト的に考えるとは、全てのソリューションや技術その他のトレードオフを見て、ベストなソリューションを決定を決定するために分析することである。「ググって出てこないこと」はアーキテクチャの要素である。
    アーキテクトはベネフィットとトレードオフの両方を知らなければならない。
    キュー設計は現行でやってるからわかるわ〜。
    - Understanding Business Drivers
    システムの成功に必要なビジネスドライバを理解し、アーキテクチャに盛り込む必要があります。
    - Balancing Architecture and Hnads-On Coding
    アーキテクトもコーディングを行い、一定の技術的深みを維持するべき。
    しかしアーキテクトのコーディング作業がクリティカルパスのボトルネックになってはいけない。しかし開発することでペインが見えるのは良いこと。
    技術的深さを維持するために
    1.PoCをいろいろやりましょう。アーキテクチャ的決定の検証になる。アーキテクチャ的特徴の比較作業もできる。プロダクションコード品質からは落とさないこと。PoCはそのまま事例になる。それ自体も良い品質のコーディング練習になる。
    2.技術的負債を巻き取る（強気だな？）。
    3.バグ改修。
    4.簡単なツール開発による自動化テコ入れ、開発チームの日々のタスク分析。
    5.コードレビュー。アーキテクトの決定が受け入れられているか確認したり、メンタリングやコーチングの機会にもなる。



### written by @hodagi
- Chap.1
    - > “Hey, I have a great idea for a revolutionary style of architecture, where each service runs on its own isolated machinery, with its own dedicated database (describing what we now know as microservices). So, that means I’ll need 50 licenses for Windows, another 30 application server licenses, and at least 50 database server licenses.”
        - ここ好き。少し前までは何をするにも費用がかかった時代だった
   - > Architecture consists of the structure combined with architecture characteristics (“-ilities”), architecture decisions, and design principles
       - アーキテクチャは、下記の四つから成り立っているという
           1. Structure: アーキテクチャのタイプ.モノリシック？マイクロカーネル
           2. Architecture characteristics: アーキテクチャ特性。システムの機能性
           3. Architecture decisions. : アーキテクチャ内の各システムに設けられた制約。ルール。DBに接続できる層はDaoだけにしましょう、的な。
               - アーキテクチャレビューボード(ARB)やチーフアーキテクトが使用するバリアンスモデルってなんのこと？
           4. 設計原則。規則というよりもこうしたらいいよというガイドライン。
 - > アーキテクトに求められる素養
     - アーキテクチャを決定する
       アーキテクチャを継続的に分析する
       最新のトレンドを常に把握する
       意思決定の遵守
       多様な露出と経験
       ビジネスドメインの知識がある
       対人スキルを持っている
       政治を理解し、ナビゲートする
       - > 大規模な顧客関係管理システムを担当するアーキテクトが、他のシステムからのデータベースアクセスの制御、特定の顧客データの保護、および他のシステムがCRMデータベースを使用しているためにデータベーススキーマの変更を行う際に問題が発生しているシナリオを考えてみます
       - 想像するだけで胃が痛いやつ...
   - ![](https://i.imgur.com/dFOjgw2.png)
   - >Another axiom is that software architecture is mostly orthogonal to the software development process; the way that you build software (process) has little impact on the software architecture (structure).
- Chap.2
    - >アーキテクチャとハンズオンコーディングのバランスをとる
アーキテクトが直面する困難なタスクの1つは、ハンズオンコーディングとソフトウェアアーキテクチャのバランスをとる方法です。私たちは、すべてのアーキテクトがコーディングし、一定レベルの技術的深さを維持できる必要があると固く信じています（「技術的幅」を参照）。これは簡単な作業のように思えるかもしれませんが、達成するのがかなり難しい場合があります。
        - これだー！！
    - ArchUnit
        - dependencyのチェック


### 雑談メモ

- 「デジタル変革企業へと転身、2022年度はDX事業で3000億円の売上を目指す」、富士通が会見
https://it.impress.co.jp/articles/-/18597
- アーキテクトはチームでやりたい
  - 専門性とチームプレー、集合知の合わせ技
- エンジニアからマネージャーへ上位互換ではないことと同様に、エンジニアからアーキテクトへ転向することは難しいことと似ている
- デベロッパーからアーキテクトに転向する方は準備することが必要
- システム開発者と利用者との間には「よいシステム」の定義に隔たりがある
  - e.g. アウトプットファイルは jsonファイルか、csv, スプレッドシート