- 「Figure 1.2 The security approach guide.」でいわれている"preimeter"と"layered"の違い
  - Source: [Concepts and Approaches | Introduction to Computer Security | Pearson IT Certification](https://www.pearsonitcertification.com/articles/article.aspx?p=2990398&seqNum=6)
  - 多層防御か -> layered
  - 範囲、横の防御か -> perimeter

- データガバナンス
  - cf. [データエコノミー時代のデータガバナンスの要諦](https://www.nri.com/-/media/Corporate/jp/Files/PDF/knowledge/publication/it_solution/2018/12/ITSF190109.pdf?la=ja-JP&hash=B829D2768FBC43406E860C723F3ADD93688CC326)

- クロスサイトスクリプティング
  - > クロスサイトスクリプティングとの違い
  - > SQLインジェクションと似たサイバー攻撃として、クロスサイトスクリプティングがあります。SQLインジェクションが、不正なコードの断片をSQLに挿入し、発動させることで直接データベースを攻撃するのに対し、クロスサイトスクリプティングは、脆弱性のあるサイトを利用し、ユーザーの個人情報やパソコンを乗っ取るのが目的です。
  - > クロスサイトという名前の通り、脆弱性のあるサイトが対象ではなく、あくまでそのサイトを踏み台にし、訪れたユーザーを別のサイトに誘導し攻撃（クロス）することから、この名前がついたとされています。
  - > クロスサイトスクリプティングでは、脆弱性のあるWebサイトにスクリプトをつけたURL（罠）などを貼っておきます。ユーザーがクリックすると、スクリプトが実行され、偽のページにリダイレクトされ、個人情報が流出したり、マルウェアに感染したりします。主に、スクリプトでは、JavaScript、htmlタグが悪用されるケースが大半です。
  - Source: [SQLインジェクションを防ぐ対策とは｜わかりやすく仕組みを解説｜セキュリティコラム｜株式会社網屋](https://www.amiya.co.jp/column/sql_injection_20200518.html)
  - cf. [偽決済画面への誘導によりクレジットカード情報を盗むデモンストレーション（Type5）](https://www.youtube.com/watch?v=y7wulJ2whQo)

- ユーザー情報はポップアップ、拡張機能から取得されている？
  - > webやアプリで便利ツールを提供する代わりに、ユーザデータを取得し、それをもとに推計して出しているのがSimilarWebです。
    - Source: [SimilarWebの数字はどれほど正確か？ SEOのプロが検証 | SAIRU NOTE | 株式会社才流](https://sairu.co.jp/doernote/0122)

- ブラウザ上の開発環境
  - cf. [Welcome! - Gitpod](https://gitpod.io/#https://github.com/prometheus/prometheus)