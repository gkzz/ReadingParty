# Chapter14. Supportive Tooling
- Supportive Toolsの目的はDevOps。scalablilityとelasticityに関わる。

## Microservice-to-Team Assignment System
- microservicesの実装とイベントストリームの主観を追跡するにはassignmentシステムが必要。人力管理は無理。

## Event Stream Creation and Modification
- イベントストリームの変更や作成はチームに適切に伝えられる必要がある。人力管理は無理。

## Event Stream Metadata Tagging
- イベントストリームのメタデータはオーナ湿布管理のためにタグ管理される必要がある。ストリームのオーナーやオーナーサービス。個人情報。ファイナンシャル。名前空間。退役。

## Quotas
- 安定稼働のためには、個々のコンポーネントがどこまでリソースを消費できるのか定める必要がある。

## Schema Registry
- サービス間でのメッセージ完全性を担保するには中央のイベントスキーマレジストリが必要。
  - マイクロサービスと言いつつスキーマレジストリで全員が密結合してるのは耐障害性的にどうなのかと毎回思っているが答えは遂に出てこない雰囲気。

## Schema Creation and Modification Notifications
- イベントスキーマの作成と変更はconsumerに通知される必要がある。

## Offset management
- 今まで出てきてなかったのが気になっていたが、supportive tooling扱いなのか。
- リセット、飛ばして進める、特定の位置にoffsetを

## Permissions and Access Control Lists for Event Streams
- event streamへの操作に対し認可の設定が必要。

## State Management and Application Reset
- これtoolingでやるの?
- 必要な機能
  - 内部ストリームと変更ログストリームの削除
  - 外部ステートストア永続化層の削除
  - コンシューマグループオフセットのリセット

## Consumer Offset Lag Monitoring
- これtoolingでやるの?
- consumer offset lagはシステムのスケールアップ(アウト)インジケータになる。
  - メトリックでのスケール制御はスパイク対応できないけど、どうするつもりなんだろうか。

## Streamlined Microservice Creation Process
- レポジトリ作成から環境セットアップまでを自動化する

## Container Management Controls
- kubernetes??

## Cluster Creation and Management
- プログラマブルにやろうね(それはそう)
- イベントブローカー、コンピュートリソース、クラスタ間レプリケーション、ツール化(そこもか)

## Dependency Tracking and Topology Visualization
- トラッキングは必要だが、トラッキングがシステム的に必要になる規模でvisualizationが成立するのか??
- トラッキングをドキュメントで行うのかシステムで行うのかいつも悩む
  - 作る前に設計としてドキュメントは必要だが、検索性を考えるとシステムとして必要で、しかし両者の一致で破綻し始める

## Summary

---

# Chapter 15. Testing Event-Driven Microservices

# General Testing Principles
- 機能テストと非機能テストが必要です
  - それはそう

## Unit-Testing Topology Functions

### Stateless Functions
- ステートレス故に関数は独立しているので関数ごとにテスト(それはそう)

### Stateful Functions
- 引数とは別に外部ストレージのデータに内部からアクセスする関数の例
  - モッキングを全てのエッジケースに対応させる必要がある

## Testing the Topology
- トポロジ＝サービスでいいのか?

## Testing Schema Evolution and Compatibility
- codeのsubmit段階でschemaのcompatibilityテストも行うこと
  - もしくは開発プロセスの中で自動化

## Integration Testing of Event-Driven Microservices
- ローカル結合テストとリモート結合テスト、もしくは混合

## Local Integration Testing
- 本番構成をローカルでも構築する必要がある。FaaSのようなものだったとしても。
  - そして独立して管理しなければならない。自力で。
  - 上手くコード化できれば任意のシナリオをローカル完結で再現させられる。

### Create a Temporary Environment Within the Runtime of Your Test Code
- テストコードの中で環境構築も行う
  - event駆動はjvm実装なケースも多いので、実質jvm言語で実装されたサービス専用

### Create a Temporary Environment External to Your Test Code
- docker composeとかminikube使えるならこれでも良いような

### Integrate Hosted Services Using Mocking and Simulator Options
- マネージドサービスはローカル用シミュレータが配布されている場合もあるので、使いましょうねという話

### Integrate Remote Services That Have No Local Options
- インフラ担当と協力して何とかするしかない

## Full Remote Integration Testing
- ローカルでは再現出来ない試験をリモートで行う。主にSLO観点。
  - レイテンシ、スケーリング、異常復帰
- 3通りの方法で行われる。

### Programmatically Create a Temporary Integration Testing Environment
- 新規環境構築の練習にもなる
- 欠点として、ストリームとデータが無い
  - どうやって本番に合わせるか

#### POPULATING WITH EVENTS FROM PRODUCTION
- セキュリティ、本番負荷

#### POPULATING WITH EVENTS FROM A CURATED TESTING SOURCE
- デザインされたデータでテストを行う
- 維持コスト、データが固定的、メンテナンス放置

#### CREATING MOCK EVENTS USING SCHEMAS
- モックでデータ生成から頑張る
- イベント間のデータ整合性担保、本番とのデータ傾向差分、本番とのデータ性質差分

### Testing Using a Shared Environment
- 意図しないデータ混ざることによる意図しない挙動
- テスト環境間でのリソース競合
- ストリームのデータ汚染
- 本番とのデータ性質差分

### Testing Using the Production Environment
- 本番影響が出た際の取り返しのつかない感
  - きれいに環境分離することは現実的か?

## Choosing Your Full-Remote Integration Testing Strategy
- 共有環境で本番相当のワークロードテストを行うと悲惨なのは解る
  - かといって環境分離したらきれいになるかと言われると確信が無い
    - イベント取得の制御をどうするかが全体的に出てこなくて引っかかっている
- オンプレとクラウドでテストの前提が変わると思うのだが、そこは考慮外なのだろうか
- この著者の構成で、部分を結合テストするということが可能なのだろうか

## Summary

- 今回もガイドライン的な話が多い
- 前から気になってたのだが、single source of truceの設計が見えない