# Fundamentals of Software Architecture Chap.3-5

- イベントページ
  - [READING.9 #技術書を英語で読む会](https://reading.connpass.com/event/194655/)
- 課題図書
  - [Fundamentals of Software Architecture: An Engineering Approach](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
- 貼っている画像の引用先
  - [Updated Fundamentals of Software Architecture Images](http://fundamentalsofsoftwarearchitecture.com/images.html)
- これまでのイベントで扱ったHackMDのリンク集
  - [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@readingparty/BJCW7wBTD)

### written by @gkzz

- Chap.3
  - 「巻物か！」と言いたくなる、pythonで書かれた長いメソッドに手を入れることがあり、どこまでメソッドとして分割してよいか迷うことがある
    - そのような書き方が複数ファイル、複数のメソッドで見受けられ、全て直したくなるが、その時間はなく、手を付けたファイルから都度直しているのが実態。。 
    - `a range of cohesion measures`はどのくらい徹底すればいいのだろう。
    - 実装に落とすとなるとイメージが浮かばない。。
       - Functional cohesion, Sequential cohesion, Communicational cohesion, Procedural cohesion, Temporal cohesion, Logical cohesion, Coincidental cohesion

  - この章でイチバン印象に残った画像。
![](https://i.imgur.com/dJJ0vRh.png  =300x)

 
- Chap.4
  - `Operational Architecture Characteristics`(Availability, Continuityなど)はAWS-SAAで知ったけど、`Structural Architecture Characteristics`(Configurability, Extensibility)と`Cross-Cutting Architecture Characteristics`(Accessibility, Archivabilityなど)は知らなかった。散乱していた知識が整理された気がする。
  - アジャイル開発から学んだことの一つが`設計の見直しを繰り返す大切さ`。くぅー。現行のシステムの設計書がどこかにいった場合はどうすれば :cry: 

- Chap.5
  - アーキテクトとビジネスサイドの責任者が使う言葉は違えど、両者が関心を持っている対象は同じ部分がある。
   > Table 5-1. Translation of domain concerns to architecture characteristics  


### written by @y-wat

- Chap.3 モジュール性
OOP真面目にやったことがないのでこの章はあまりイメージつかない。。。
    - 定義
モジュール性: 関連するコードの論理的集合。OOPでのクラスのグループや関数型言語での関数。物理区分ではない。(物理ってなんのことだ)
    - モジュール性を計測する
        - 凝縮
同じモジュールに含まれるべきモジュールの部分(?)。パーツがどれくらい相互関連しているか。分割すると結合(coupling)が必要になる。
functional cohesion
sequential cohesion
communicational cohesion
procedural cohesion
temporal cohesion
logical cohesion
coincidental cohesion
notify customerは別にするなぁ
LCOM
LCOMが低いほうが良い？高いとcohesion。高いほうがアーキテクチャ変更しにくくなると思うが。
        - 結合
        - 抽象性、変わりやすさ、main sequence(?)からの距離
        - main sequence(?)からの距離
        - connascence (OOPでのソフトウェア品質を示す依存関係による複雑度指標)
            - static connascence
            - dynamic connascence
            - connascence properties
        - Unifying Coupling and Connascence Metric
            - the problems with 1990s connascence
    - from modules to components
- Chap.4
無視して突っ走る人多いよな。なんでだろう。
直接のドメイン機能ではないがソフトウェアとして実施しなければならないこと: アーキテクチャ的諸特徴
・非ドメインのデザイン考慮を特定する（explicit）
・デザインの構造的側面に影響を与える(implicit)
・アプリケーションの成功に決定的または重要である
    - アーキテクチャ的諸特徴のリスト
        - 操作的(?)なアーキテクチャ的諸特徴
        availability, continuity, performance, recoverability, reliability/safty, robustness, scalability
        devopsと被る
        - 構造的なアーキテクチャ的諸特徴
        configurability, extensibility, installability, leverageability/reuse, localization, maintainability, portability, supportability, upgradeablity
        コーディング寄りの内容
        - 横断的なアーキテクチャ的諸特徴
        accessibility, archivability, authentication, authorization, legal, privacy, security, supportability, usability/achievability
    - トレードオフと再小悪のアーキテクチャ
    あるアーキテクチャ上の考慮が他の要素にネガティブな効果を出すことも有る。トレードオフに対する決定が必要。アーキテクチャもイテレーティブな対応が必要。
- Chap.5
    - ドメインの関心からアーキテクチャ的諸特徴を抽出する
    ファイナルリスト(?)を短く保つのが良い(関心を絞る) 
    汎用アーキテクチャを作るのはアンチパターン
    ドメイン関係者とアーキテクトの間で用語を揃える必要がある
    - 要件からアーキテクチャ的諸特徴を抽出する
    アーキテクチャの型(詳細、ユーザ、要求、追加的背景)
    - ケーススタディ
        - 明示的な特徴
        型のユーザセクションで表された、期待されるメトリックに対するドメインレベルでの想定を考慮すべき
        要求に記載がなかったとしても、潜在的なアーキテクチャ的諸特徴をアーキテクトは特定すべき（ex. スケールしか記載がなくてもサービスの性質からエラスティックに対する要求を推測する）
        要求がニュアンス的なものであったり、相互に関連している場合もある。ベースラインを定めたり関連性を明確にする動きがアーキテクトには求められる。
        - 暗黙的な特徴
        完全に正しいアーキテクチャ的諸特徴の組み合わせの発見を強調しすぎるべきではない。重要な構造的要素を正確に毒挺することはエレガントなデザインを用意にする。ベストなデザインはアーキテクチャに存在しないが、再小悪のトレードオフは存在する。
        最もシンプルな要求を発見することに向けてアーキテクチャ的諸特徴を優先しなければならない。

### written by @fujiwara

- Chap.3
    - 他の凝集の結果、直接的に関係のない要素がモジュール内で混在している状況？
        - Coincidental cohesion
            - Elements in a module are not related other than being in the same source file; this represents the most negative form of cohesion.
    - 結合
        - Structured Design: Fundamentals of a Discipline of Computer Program and Systems Design (Prentice-Hall)
            - afferent/efferent
- Chap.4
    - Maintainerbility?とか、Operational Service Level?
        - Operational Architecture Characteristics
            - Robustness
                - Ability to handle error and boundary conditions while running if the internet connection goes down or if there’s a power outage or hardware failure.
    
- Chap.5
    - やりがち。自身が運用経験がある方法を、汎用的に適用しようとしたり。
        - A common anti-pattern in architecture entails trying to design a generic architecture, one that supports all the architecture characteristics. 
    - Case Study: The Vasa → 日本だと大和とか。実際に活用される場面を想定(戦いであれば戦術レベル)しないと、特定の特徴や性能のみが秀でていて、期待した成果を挙げられない(期待している成果も曖昧そう)。
    - 人が1度に覚えられるのは3つまで。多分、本人が熱く語っても4つ目以降は冗長で聞かれていないのがほとんどなので、こういう線引きが必要。政治的な話。全員が3つ持ち寄るんじゃ無くて、決済者に3つ出させる。
        - Rarely will all stakeholders agree on the priority of each and every characteristic. A better approach is to have the domain stakeholders select the top three most important characteristics from the final list (in any order).

### written by @hodagi

- Chap.3
    - jarの悲劇..この経緯なんか笑った。
    - https://www.maibornwolff.de/en/blog/connascence-rules-good-software-design
    - Connascence https://connascence.io/
- Chap.4
    - Operational Architecture Characteristics
    - Structural Architecture Characteristics
    - Cross-Cutting Architecture Characteristics
    - ITALY-ILITY(mobILITY)みたいなものか。
        - 確か東京がなくなると、日本のインターネットは死ぬんでしたっけ(NTT的な意味で)
    - ドメイン駆動からチーム内でのみ通じる用語への変化
    - 逆にISOのそれが漠然とした感じを受けるのは何でなのかな。
- Chap.5
    - Translation of domain concerns to architecture characteristics
        - 先日読んだサイボウズさんのSLOに関する考え方が、オペレータとしての観測のしやすさとユーザーの満足度で揺れていて個人的にその葛藤が同感してしまったな
    - スケーラビリティーとパフォーマンス=弾力性..わかる。
    - THE ORIGIN OF ARCHITECTURE KATAS


### 雑談メモ

- [connascence.io](https://connascence.io/)
- 開発履歴は追えるけど最新の仕様はキャッチアップできない
- issueという変更履歴の積み重ねが最新の仕様なのだけど。。