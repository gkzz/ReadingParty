# Chapter 13. Integrating Event-Driven and Request-Response Microservices
- Req/Res型はイベント駆動ではない扱いなのか。

## Handling External Events
- 外部から生成されるイベントは2種類(以下)

### Autonomously Generated Events
- メトリック系
  - 分析的イベント: 計測結果や事実についてのステートメント

### Reactively Generated Events
- こちらからのリクエスト結果

## Handling Autonomously Generated Analytical Events
- イベントがスキーマ定義されていることが重要
- clinetとstreamの中継を想定しているのかね?

## Integrating with Third-Party Request-Response APIs
- in stream -> api call -> out stream
- async api callできるのは処理順序に依存がない場合のみ
- 対向へのcall負荷を考慮しましょう

## Processing and Serving Stateful Data
```there is only one microservice instance, and since it is materializing all of the state data for this application```
- インスタンスごとに永続層を固定する設計、どうなんだろうか

### Serving Real-Time Requests with Internal State Stores
- スケーリングどうやってやるのか全く想像がつかない
  - インスタンス数調整とシャード割当を同時に触る??
  - パーティショニングとmicro serviceって関係無いよねと思った(event drivern要因)

### Serving Real-Time Requests with External State Stores
- パーティション戦略とストレージ戦略が分離できる
  - いいじゃないか

#### SERVING REQUESTS VIA THE MATERIALIZING EVENT-DRIVEN MICROSERVICE
- eventからの永続化とclientからの読み出しを同じmicroserviceで行う
  - clientからの書き込みは考慮しない??

#### SERVING REQUESTS VIA A SEPARATE MICROSERVICE
- eventからの永続化とclientからの読み出しを違うmicroserviceで行う
  - clientからの書き込みは考慮しない??

## Handling Requests Within an Event-Driven Workflow
- 方法1. リクエストを直接永続化する
- 方法2. 一旦イベントストリームを経由させる

### Processing Events for User Interfaces
- asyncronous UIは時間がかかる(そうなのか)
- asyncronous UIの考慮
  - 待機画面でユーザの操作を制限する
  - バックエンドとの常時通信をいつ表に出すか

#### EXAMPLE: NEWSPAPER PUBLISHING WORKFLOW (APPROVAL PATTERN)

#### SEPARATING THE EDITOR AND ADVERTISER APPROVAL SERVICES
- (感想)単に小さいサービスをストリームで繋ぐのは難しくはない。面倒なのは以下が要件に入ってきたときでは。
  - 障害時の欠損対応
  - 待ち合わせ
  - 過去データの再走行

## Micro-Frontends in Request-Response Applications
- マイクロフロントエンドもreq/res型マイクロサービスに入れるのか
- マイクロフロントエンド
 - フロントも独立した構成にしてしまう
 - 個別フロントコンポーネントは専属のバックエンドを持つ

## The Benefits of Microfrontends
- separation of business concerns
- autonomous teams
- and deployment, language, and code-base independence

### Composition-Based Microservices

### Easy Alignment to Business Requirements

## Drawbacks of Microfrontends

### Potentially Inconsistent UI Elements and Styling
- 単一の画面を複数のモジュールからくみあげるので、UIの統一感を保つのが難しい

### Varying Microfrontend Performance
- 個々のコンポーネントでfailureがあっても、全体としての体験を損なわずにいられるか

### Example: Experience Search and Review Application

## Summary


# 感想
- 結局の所、apiとして受けても即座にstreamへ変換するので、req/resを強調する必要もない気がした
- いつも思うのだが、change logを再走行する仕組みってどうしてるんだろうか
- (感想)単に小さいサービスをストリームで繋ぐのは難しくはない。面倒なのは以下が要件に入ってきたときでは。
  - 障害時の欠損対応
  - 待ち合わせ
  - 過去データの再走行
- 結局のところ、リージョン障害に耐えつつexactry onceを保ちつつ、後々の全量再走行にも耐える設計というのが全く見えてこない