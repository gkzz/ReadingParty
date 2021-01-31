# Building Secure & Reliable Systems Chap.4-6

- イベントページ
  - [READING.6 #技術書を英語で読む会](https://reading.connpass.com/event/191984/)
- [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@gkzz/H1fdY9jOP)
- [Building Secure &Reliable Systems](https://static.googleusercontent.com/media/landing.google.com/en//sre/static/pdf/Building_Secure_and_Reliable_Systems.pdf)

### written by @gkzz

- [Ch4] 機能要件と非機能要件の二兎を負うとなると、Development efficiency and velocityとDeployment velocityが失われかねないというところに共感
  - 二兎を意識して開発の効率性が損なわれることは普通。三兎はおろか二兎すら追わないですよね？ｗ
  - 開発の文脈でいうvelocityの意味は、下記のMcKinseyの`Developer Velocity`に関する説明でいうところのエンジニアの能力を引き出すニュアンスだと理解
  - ~~開発者の能力が削がれる業務設計、組織体系となっているなぁ~~
 > Improving business performance through software development comes down `to empowering developers,` 
 > creating the right environment for them to innovate, and removing points of friction. 
 > Industry leaders refer to this capability as `“Developer Velocity.”` 
 > This goes beyond the definition of velocity as it relates to agile methodologies—meaning 
 > it is about `not just speed but also unleashing the full potential of development talent.`

出所：[How software developers can drive business growth | McKinsey](https://www.mckinsey.com/industries/technology-media-and-telecommunications/our-insights/developer-velocity-how-software-excellence-fuels-business-performance#)

- [Ch5] 開発時に使うテスト環境の権限は全振り？インターン生の権限は同じロールの社員と違う？
- 取り上げられていた「Ambient Authority」とは？
> 間接的な権限の一種。例えば新聞記者に与えられる記者証のようなものと考えてもいいかな。記者（人間）が「私は権限がある！」という代わりに、記者証をチラっと見せるとき、実際は別の人間が成りすましていたとしても何も聞かずにどうぞそうずと部屋に入れてしまう、そういう感じのこと。

出所：[RESTFulなAPIとCSRFとその対策](https://watanabe-tsuyoshi.hatenablog.com/entry/2015/03/04/123649)
-> 代理

- [Ch6]「Figure 6-3. Example microservices architecture for widget-selling application」のように、求められるセキュリティの程度に応じてデータベースの構成を分けるというお話は大事だなと。↓で引用されている「ピタゴラスイッチ」のようなことは既視感があり汗。
> “新商品の追加を行うと、PC版でカスタマーの新規登録ができなくなる。”
> 『Pairsの開発中の話』より （共著: 小島ヒロキ・森川タクマ）

出所： [[Go言語での決済システムとマイクロサービス化について](https://link.medium.com/2Z03dD5ZEab )

### written by @fujiwara
#### Ch5 
- 「Design for Least Privilege」での最初の部分「希望は戦略では無い」は大事な断りだと感じた。同様に主観でよく使われる「倫理観、常識、当たり前、普通」などの対象を明文化せずに期待する甘えは、セキュリティーでは通用しない。Googleの文章ではこういう用語や概念の認識合わせがちゃんとされて助かる。→Initial Velocity vs Sustained Velocityなどと繋がる。整合性がある。
> Even if we generally trust the humans accessing our systems, we need to limit their privilege and the trust we place in their credentials. Things can and will go  wrong. People will make mistakes, fat-finger commands, get compromised, and fall for phishing emails. Expecting perfection is an unrealistic assumption. In other words— to quote an SRE maxim—hope is not a strategy.
- チームレベルでの権限行使の相互レビュー、breakglassチェックしていますか？
  - 作業の実施と終了時の権限付与の妥当性と剥奪は管理している。また、AWSマネージドサービスと内製ツールで不要なリソース、IPやポートの公開、信頼関係などを監視している。メンバーレベルでは、レビューの時間は個別に作っていない。
> Google typically distributes breakglass reviews down to the team level, where we can leverage the social norming that accompanies team review.

> Before building a multi-party authorization system, make sure the technology and social dynamics allow someone to say no. Otherwise, the system is of little value.

> As an example, consider a customer service workflow. In an anti-pattern sometimes found in small or immature organizations, a basic and nascent system may give cus‐ tomer service representatives access to all customer records, either for efficiency rea‐ sons or because controls don’t exist. A better option would be to block access by default, and to only allow access to specific data when you can verify the business need. This approach may be a gradient of controls implemented over time. For exam‐ ple, it may start by only allowing access to customer service representatives assigned an open ticket. Over time, you can improve the system to only allow access to specific customers, and specific data for those customers, in a time-bound fashion, with customer approval.

#### Ch6 
- Team TopologiesのCognitive Loadを思い浮かべた。あちらは組織論。 

### written by y-wat

#### Ch4
- tradeoffとは言うものの、個人情報とか決済不具合を除いて「ごめんなさい」で済んでしまってる感無い？
- ソフトウェアって言うほどホイホイ乗り換えるものだろうか(=一度囲ってしまえば暫くは勝てる)
- 実態としては「他社より酷くない」サービスレベルを目指す？
> GOOGLE’S DESIGN DOCUMENT TEMPLATE
- ↑うちは整ってないですね
- 立ち上がり期の開発速度優先すると後々のセキュリティとかreliability対応で開発速度が落ちるというのは解るリファクタ辛い

#### Ch5
- 内部犯ってどうしたらいいの
- 最小限の権限って会社全体で見通してないと意味ないよね
- CI/CD鯖の最小権限とは
- 最小限ってどこまでで最小限？ ex (rdb). table? column? row? cell?
    - 探索的作業の場合は？
- securityとかreliabilityって技術というより組織文化色のほうが強くない？
- 都度権限与えたり剥奪したりって意味有るのかな。却下オペが実質ない場合。

#### Ch6
- アーキテクチャをシンプルに抑え込めるかで難易度変わるよね問題
- 適切な設計をしていれば、サービス境界とauthのセキュリティ境界は一致する気がするものだが
