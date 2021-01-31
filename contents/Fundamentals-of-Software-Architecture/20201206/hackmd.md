# Fundamentals of Software Architecture Chap.12-13

- イベントページ
  - [READING.12 #技術書を英語で読む会](https://reading.connpass.com/event/196715/)
- 課題図書
  - [Fundamentals of Software Architecture: An Engineering Approach](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
- 貼っている画像の引用先
  - [Updated Fundamentals of Software Architecture Images](http://fundamentalsofsoftwarearchitecture.com/images.html)
- これまでのイベントで扱ったHackMDのリンク集
  - [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@gkzz/H1fdY9jOP)


### written by @gkzz

- Chap.12
  - > The microkernel architecture style is a relatively `simple monolithic architecture consisting of two architecture components: a core system and plug-in components.`
![](https://i.imgur.com/8KPVTzt.png =300x)
  - [songumuさんのTweet](https://twitter.com/songmu/status/1334456791510339585?s=20)をチラ見していたことを思い出した。
    - > 将来的に技術が順当に進化したらやらなくて良くなることを、その場しのぎで解決してしまうの後々負債になってしまうし、やるにしても将来どうなるかを見越して `「取り外せるように作る」` のが大事だよな。 
  - こと「疎結合」といってもcomponents間で「従属、依存」？といってもよい関係がある。
  - `the size and complexity`（従属、依存関係）の度合いが大きいと`the core system`はモノリシックな傾向がある。
    - e.g.例に挙げられているエディタとプラグイン。決済アプリと通販。
  - `volatile` (adj)
    - meaning: 
      - (of a computer's memory) retaining data only as long as there is a power supply connected. 
      - liable to change rapidly and unpredictably, especially for the worse: the political situation was becoming more volatile.
  - > Compile-based plug-in components are `much simpler to manage but require the entire monolithic application` to be redeployed when modified, added, or removed.
    - cf.[バージョンアップ時に互換性を損ねてしまう変更](https://irof.hateblo.jp/entry/2016/01/06/215707)
      - > ありとあらゆる互換性を維持するなんて愚かな目標を立てるべきだと言いたいわけではありません。それは変更を、つまり成長を阻害することとイコール
      - > 変更がどのような互換性を損ねるかを把握し、 問題があった時にどう対応すれば良いか、その対応にどのくらいかかりそうか とかを 考えといた方がいい 
  - `Wildfly`
    - cf.[わいるどふらい(WildFly)って何？から学ぶEJB](https://ponsuke-tarou.hatenablog.com/entry/2018/05/29/002359) 
      - > WildFlyは、オープンソースJavaEEアプリケーションサーバ
      - > WildFly（ワイルドフライ）とは、`JBoss AS（コミュニティ版）とJBoss EAP（エンタープライズ版）との混同を避けるため2014年4月にJBoss ASが改名された名称`
      - > その為、名称が変更されたのみとなっており、開発コミュニティ（オープンソースプロジェクト）やソフトウェア自体などJBoss ASと変わりません。 
  - ![](https://i.imgur.com/78gJUQm.png =300x)

- Chap.13 
  - > The basic topology of service-based architecture follows a distributed macro layered structure consisting of a separately deployed user interface, separately deployed remote coarse-grained services, and a monolithic database.
    - cf. [サービス指向アーキテクチャ (SOA) とは](https://www.redhat.com/ja/topics/cloud-native-apps/what-is-service-oriented-architecture)
      - > ネットワーク上の共通の通信言語を使用するサービスインタフェースを介してソフトウェアコンポーネントを再利用可能にするソフトウェア設計の一種
    - cf.[2.2 サービスベースアーキテクチャ |
NTTドコモ](https://www.nttdocomo.co.jp/corporate/technology/rd/tech/5g/5g06/02/02.html)
      - > 5Gコアネットワークアーキテクチャでは、ノード間の連携に着目した場合の、5G実現方式としてサービスベースアーキテクチャが採用された] 
    - cf. [モノリシックからマイクロサービスへ。あるいは、サービスベースアーキテクチャを考える。
](https://tech.askul.co.jp/entry/2019/04/09/132952)
      - > サービスベースアーキテクチャとは(中略)サービスのサイズを大きくし、データベースの独立性を保ち、他レガシーシステムとうまく連携 (中略) "可能な限り共有の少ない"アーキテクチャ
      - > マイクロサービスで幸せになることができるのか。それは組織の成熟度やシステムの状況など、さまざまな課題がある (中略) そして、課題の数だけアーキテクチャが存在 (中略) ShopifyからはModular Monolithsという「単一のコードベースの中にドメインごとの境界を作る」考え方も提唱
  - `facade` noun
    - meaning: the principal front of a building, that faces on to a street or open space.
      - e.g."the house has a half-timbered facade"
      - Syn: front, frontage, face, aspect, elevation, exterior, outside 
  - サービスの粒度とトランザクション制御
    - `粒度が荒ければACID、細ければBASE`
      - cf.[マイクロサービスの粒度](https://qiita.com/soichiro0311/items/cee322fc61b4a5c63af5)
        - > 分割したサービスが複数のサービスのデータベースにまたがってトランザクションを保持しなければEventually Consistentを担保できないならば、サービスの粒度を大きくすることを検討
  - > ![](https://i.imgur.com/jL03EvJ.png =300x)
    - > For example, the Assessment service is changed constantly to add assessment rules as new products are received. 
  - ![](https://i.imgur.com/ZTq8Ges.png =300x)
 

### written by y-wat

- Chap.12 Microkernel Architecture
プラグインアーキテクチャ
シングルなモノリスパッケージとしてインストールして利用する製品に適合する
    - Topology
    core systemとplug-in componentsで構成
        - Core System
        例: Eclipse IDE(テキストエディタ機能のみ)
        機能ごとにプラグインとして隔離することで拡張性が保たれる
        core systemはレイヤードアーキテクチャまたはモジュラモノリスとして実装される
        ユーザインタフェースは同じ筐体の場合も別所の場合もある
        - Plug-In Components
        個別のPlug In Componentは独立したコンポーネントであり、メンテナンス性やテスト性を高める
        coreとplug inのrestパターンは分散ではないのか？(コアがモノリスだから、というのが理由らしい) -> 近づくという見方はある
        rest越しになるとアーキテクチャの複雑性は増す
        ストレージはコンポーネントごとに分ける
    - Registry
    コアシステムからどのプラグインが利用可能でどのように利用するのかを管理する
    - Contracts
    コアとプラグイン間での振る舞い、データin/outの標準取り決め
    - Examples and Use Cases
    Eclipse, Jira, Jenkins, browser等々で使われている
    big ball of mudになりそうな大規模環境でも効果はあるかも
    - Architecture Characteristics Ratings
    (この星は真面目に見るべきなのか)
- Chap.13
    - Topology
    複数の独立デプロイされるドメインサービスから構成される(サービスは数個から10個強)
    サービスは独立しているが、データベースは共有
    - Topology Variants
    UIは単一〜サービスごと独立まで
    DB分割もやたりやらなかったり
    UIとサービスの間にAPIでゲートウェイする場合もある
    - Service Design and Granularity
    個々のサービスはレイヤード、またはモジュラモノリスが一般的
    インターナルなクラス間連携か、外部との連携が必要になるのかでサービスベースアーキテクチャとマイクロサービスは異なる
    サービスベースアーキテクチャはACIDで対応する
    マイクロサービスはBASEで対応する（にわとりひよこな気もするが）
    あー、サービスの考えが大きめなんだな
    - Database Partitioning
    SAでは共有された個別クラスファイルがDBスキーマに対応する
    DBスキーマへの変更はライブラリを共有するオブジェクト全体に波及する
    DBを論理的にパーティショニングすると良い(パーティショニング機能を使えということなのか、スキーマから割れということなのか？後者なはず。)
    - Example Architecture
    マイクロサービスのTCCパターンと近い匂いがする。テーブルをサービス間で共有しているかどうかで分かれ目な気がする。
    - Architecture Characteristics Rating
    ドメイン間で独立させるのは良いとして、ストレージ層を共有させるか迷いますよねぇ
    - When to Use This Architecture Style
    フレームワーク組み込みのORM使うと採用しづらい気はした(migrateがつらそう)


### written by @fujiwara

- Chap.12
    - Microkernelと聞いていて、[Unikernel/MicroVM](https://speakerdeck.com/inductor/microvm-and-unikernel-in-the-container-world)が頭に浮かんじゃいました。全く違う話。
- Chap.13
    - Database Partitioning
        - Make the logical partitioning in the database as fine-grained as possible while still maintaining well-defined data domains to better control database changes within a service-based architecture.

### written by @hodahgi
- Chap.12
    - [MINIXの30年の歴史から学んだこと_原題: Lessons learned from 30 years of Minix_](http://member.wide.ad.jp/~shima/publications/Lessons_learned_from_30_years_of_Minix-JP.html) が浮かんじゃいました。


## 雑談

今回はメモすることが多かったのでサマリーをっ
- > ApplieのA1のようにエッジコンピューティングでの性能が上がり、安くなる
    エッジコンピューティングがさかんになる。
    分散トランザクションが必要になる。
    ブロックチェーンの改ざん検知とデータ追跡用が利点として認められる
    ブロックチェーンつまり来る！
- [「フロントエンド領域」を再定義する](https://speakerdeck.com/mizchi/hurontoendoling-yu-wozai-ding-yi-suru?slide=49)

---------------

>ユーザにより良いサービスを提供するため、MITは互換タイムシェアリングシステム (Compatible Time-Sharing System、CTSS) と呼ばれる仕組みを開発しました。

を読みまして。

- Facebookのとある投稿
  - > 銀行の過去履歴62日分しかない
    > → 再発行依頼
    > → 1ヶ月分550円
    > → 紙でしか渡せない
    > → 紙に印刷されたものをPCにうちなおす
    > ↑イマココ
    > このアホみたいな作業をなんで銀行は強要してくるのだろう…。
    > 支店単位っていうのも意味わかんないすよねー…
  - コメント
    - > インターネットがない時代、支店ごとにホストコンピュータとシステムを作っていた？あるいは吸収合併で別システムを用いていた別の銀行の支店だったが名前だけが合併先の銀行に変わった

- [UNIXという考え方―その設計思想と哲学](https://www.amazon.co.jp/dp/4274064069)
- [モノリシックカーネル](https://www.wikiwand.com/ja/%E3%83%A2%E3%83%8E%E3%83%AA%E3%82%B7%E3%83%83%E3%82%AF%E3%82%AB%E3%83%BC%E3%83%8D%E3%83%AB)
- [マイクロサービス→マクロサービスに移行したUber](http://highscalability.com/blog/2020/4/8/one-team-at-uber-is-moving-from-microservices-to-macroservic.html)
  - > マイクロサービスで幸せになることができるのか。それは組織の成熟度やシステムの状況など、さまざまな課題があると思います。 そして、課題の数だけアーキテクチャが存在するということです。ShopifyからはModular Monolithsという「単一のコードベースの中にドメインごとの境界を作る」考え方も提唱されています。 
  - > モノリシックからマイクロサービスへの移行へ、一足飛びに行うんじゃなくてその間にA、B、Cくらい中間遷移に名前をつけたい 
- トランザクション、データの処理が散らかる
- ネットワークのレイテンシー遅い
  -> 書き込みのサービスから読み込みのサービスの箇所がネック
  ->「書き込んだら、xxのページを確認してね」と誘導 

- [今後は「データ指向アプリケーションデザイン」を考えよう(Red Hat Forum講演フォローアップ記事)](https://rheb.hatenablog.com/entry/data-intensive-application)
  - ![](https://i.imgur.com/Gi0rSmb.png =300x)
  - ![](https://i.imgur.com/W636Pcq.png =300x)
  - ![](https://i.imgur.com/4V7oy7B.png)
- [Spanner から GKE、Spinnaker、そして SRE まで、コロプラが今挑戦していること[Google Cloud INSIDE Games & Apps]](https://www2.slideshare.net/GoogleCloudPlatformJP/spanner-gkespinnaker-sre-google-cloud-inside-games-apps/61)
  - ![](https://i.imgur.com/gLl0s9u.png =300x)
- [お知らせ: Google Cloud の Buildpacks でコンテナ イメージ作成が簡単に](https://cloud.google.com/blog/ja/products/containers-kubernetes/google-cloud-now-supports-buildpacks)
- [ONNX and Azure Machine Learning: Create and accelerate ML models](https://docs.microsoft.com/en-us/azure/machine-learning/concept-onnx)
- [第2章 Source-to-Image (S2I) OpenShift Container Platform 3.9 | Red Hat Customer Portal](https://access.redhat.com/documentation/ja-jp/openshift_container_platform/3.9/html/using_images/source-to-image-s2i)
- [AppleシリコンM1チップはなぜこれほど速い？ソフトウェア開発者が分析](https://japanese.engadget.com/apple-silcon-m1-sofast-why-030010404.html)
  - > Appleシリコン「M1」チップは高いパフォーマンスが続々と証明されつつありますが、なぜこれほど速いのか？　それを考察して深く掘り下げたソフトウェア開発者の分析が公開されています。
- [0からRust/Wasmを使ってブラウザで動くバーコードリーダを作ってみた話 @_mkazutaka](https://engineering.mercari.com/blog/entry/20201203-abe6f311b1/)
- [WebAssemblyでの機械学習モデルデプロイの動向](https://tkat0.github.io/posts/deploy-ml-as-wasm/)
- [#CNCF TOC chair @lizrice is sharing the 5](https://twitter.com/CloudNativeFdn/status/1329863326428499971)
- [「フロントエンド領域」を再定義する](https://speakerdeck.com/mizchi/hurontoendoling-yu-wozai-ding-yi-suru?slide=49)
  - ![](https://i.imgur.com/kanBcBG.png =300x)
  - ![](https://i.imgur.com/rPS2RLQ.png =300x)
- [PWA（Progressive Web Apps）の現状とその開発方法](https://www.mitsue.co.jp/knowledge/blog/frontend/201702/23_2217.html)
- [スーパーアプリ入門。Wechat、AliPay、GoJekが提供するプラットフォームの新しい形とは](https://yapp.li/magazine/3622/)
- [Epic Games対アップル訴訟](https://ja.wikipedia.org/wiki/Epic_Games%E5%AF%BE%E3%82%A2%E3%83%83%E3%83%97%E3%83%AB%E8%A8%B4%E8%A8%9F)
- [BigchainDB 2.0 – ブロックチェーンベースの分散型データベース](https://gaiax-blockchain.com/bigchaindb2)
- [MLSE モバイル向け機械学習モデル管理基盤](https://speakerdeck.com/yujioshima/mlse-mobairuxiang-keji-jie-xue-xi-moderuguan-li-ji-pan)
- [TensorFlow を選ぶ理由](https://www.tensorflow.org/js/tutorials?hl=ja)
  - > TensorFlow.jsは ブラウザとNode.js内で 機械学習モデルの訓練とデプロイを行うための JavaScriptライブラリ
- [Tensorflowの転移学習サンプルを機械学習の初心者がギリ分かるところまで噛み砕いてみた](https://dev.classmethod.jp/articles/introduce-to-transfer-learning-by-tensorflow-for-beginner)
  - > 転移学習、というのはざっくり言うと「元々学習されているモデルを使って自分たちの使いたい方向に再学習すること」です。 
