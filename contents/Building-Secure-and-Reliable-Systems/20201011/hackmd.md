# Building Secure & Reliable Systems Chap.2

- イベントページ
  - [READING.5 #技術書を英語で読む会](https://reading.connpass.com/event/190762/)
- [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@gkzz/H1fdY9jOP)
- [Building Secure &Reliable Systems](https://static.googleusercontent.com/media/landing.google.com/en//sre/static/pdf/Building_Secure_and_Reliable_Systems.pdf)

### written by @gkzz

- ブラックリスト(IPなど)みたいなものって企業間で共有している？
- あるいはセキュリティベンダーが持っているから外注する？
- 自前でセキュリティ周りをやらずにSaaSを使うという前提での自衛ナレッジがあるとしたら、なんだろう？
- OSSなどサードパーティー製品を媒介として、サードパーティー製品の開発者がインサイダー攻撃をおこなうというケースは今後も増加傾向を辿るはず。
- `ハッカーと敵対するのではなく協業する`というやりかたをChrome開発プロジェクトでは行われているらしい。協業関係にするというのは、具体的にはハッカーのモチベーションをバグを見つけることに転換させるところだと考える。
  - cf.[Chromeセキュリティバグを見つけたらGoogleから報奨金もらえる](https://jp.techcrunch.com/2019/07/20/2019-07-18-google-will-now-pay-bigger-rewards-for-discovering-chrome-security-bugs/)
  - cf.[55:10 Chromeの脆弱性報奨システム | 25. Chromeのローディングの最適化、脆弱性報奨システム、ブラウザとマイクロカーネル](https://turingcomplete.fm/25#t=55:10)

### written by @y-wat

- 最小権限の原則って実際守ってます？
- アプリケーションのセキュリティ開発標準(？)みたいなのを策定する専門部署って有ります？
- 開発部署でも独自にセキュリティの話を追ったり対応してます？「社内標準守ってるからヨシ(๑•̀ㅂ•́)و✧」？
- `System designers should carefully consider whether they could be the target of a nation-state actor`
    - :innocent: 
- :thinking_face: 

### written by @fujiwara
- OSSの脆弱性とか、バージョンの互換性ってどの程度まで検証していますか？
    - Terraformとか、Kubernetesとかのバージョンアップでバグを踏んだり、意図しない挙動でダウンしそうな気がする
- Google検索で検出条件に"/"を差し込んで全サイトに“This site may harm your computer”が表示されたのは、似た様なことはいくらでもあると思う。フェイルセーフどこまでやるか。