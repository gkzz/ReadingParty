- [pingでMTUサイズを調査する：Tech TIPS - ＠IT](https://www.atmarkit.co.jp/ait/articles/0512/17/news017.html)
  - > ネットワークで通信を行う場合、（通常は）一度に送信可能なデータ（パケット）のサイズには上限がある。例えば、TCP/IPプロトコルで利用されているIPプロトコルでは、1つのIPパケットでは最大64Kbytesまでしか送信できない（IPv4の場合）。

- [DDoS攻撃について教えてください。 | Questionbox](https://peing.net/en/q/8d995b56-837d-41ab-9c65-bd8dd0e11c4f)
  - > 結論から言うと「一般的な対策」は「何もせず放置」です。

- [サイバー攻撃等の遮断等に係る検討について](https://www.jaipa.or.jp/other/mtcs/guideline_v5.pdf)
  - DDoSの遮断と通信の秘密について
- [ブラックホール持続時間の確認 - Anti-DDoS Origin| Alibaba Cloud ドキュメントセンター](https://jp.alibabacloud.com/help/doc-detail/40044.htm)
  - > サーバーが大規模な DDoS 攻撃を受け、ブラックホール機能がトリガーされると、サーバーのセキュリティ信用力に基づいて、サーバーのパブリック IP アドレスは一定期間無効になります。
- [【清水理史の「イニシャルB」】 ［HowTo］中国のグレートファイアウォールを突破する方法 - INTERNET Watch Watch](https://internet.watch.impress.co.jp/docs/column/shimizu/653642.html)

- [IPスプーフィングとは？ | Cloudflare](https://www.cloudflare.com/ja-jp/learning/ddos/glossary/ip-spoofing/)
  - > 偽造ソースアドレスの偽装IPパケットは、検出されることを回避するために攻撃でよく用いられます。

- [Linux におけるソケット数 (TCP のコネクション数) の上限](https://www.yunabe.jp/docs/maximum_number_of_sockets.html)

- [43. WebTransport、HTTP/3、WebCodecs w/ yuki_wtz](https://fukabori.fm/episode/43)
- [WebAssembly wiki](https://ja.wikipedia.org/wiki/WebAssembly)

- [TCP/IP - TCPとは - TCPヘッダ](https://www.infraexpert.com/study/tcpip8.html)
  - > TCPセグメント（TCPパケット）は以下の通り「TCPヘッダ」と「TCPペイロード」で構成されます。TCPヘッダの中身は以下です。TCPペイロードはTCPより上位のプロトコルを含むデータのこと
  - > TCPヘッダのフィールドにある「コントロールフラグ」の6bitの詳細

|ビット       |値が「1」である（フラグが立っている）時の意味    |
|------------|------------------------------------------|
|URG (Urgent)|緊急に処理すべきデータ含まれていることを意味する。|
|ACK (Acknowledgement)|	　確認応答番号のフィールドが有効であることを意味する。コネクション確立時以外は値が「1」。|
|PSH ( Push )|受信したデータをバッファリングせずに、即座にアプリケーション（上位）に渡すことを意味する。|
|RST ( Reset )|コネクションが強制的に切断されることを意味する。何らかの異常を検出した場合に送信される。|
|SYN ( Synchronize )|コネクションの確立を要求することを意味する。|
|FIN ( Fin )|コネクションの正常な終了を要求することを意味する。|

- [セッションとコネクションは何が違う？ - 意外と知らないネットワーク用語の違い：日経クロステック Active](https://active.nikkeibp.co.jp/atclact/active/17/030800250/030800010/)
  - > セッションは、もっと狭い意味でも使われる。狭義のセッションとは、一連のHTTPメッセージを管理することである。こうすることで、あるユーザーが行っているWebアクセスを認識し、画面表示や決済の状態を把握する。
  - > 一方のコネクションは、通信している者同士が仮想的な接続状態を確立することをいう。一般にコネクションといえば、TCPコネクションを指す。TCPはこのコネクションを作り出すことで、通信の確実性を実現しようとしている