# Chapter 9. Microservices Using Function-as-a-Service

## Designinng Function-Based Solutions as Micorservices
- Bounded Contextを遵守する
- イベントの処理完了前にstream側にコミット通知しない
  - 標準的なFaaSなら、そんな事態にはならないはずだが??
  - というかこれってFaaSに限った話じゃないよね
- fragmentedを避ける
  - FaaSは仕方ないんじゃないかな

## Building Microservices Out of Functions
- functionのmetadata
  - funcation name
  - 上流event stream
  - trigger
  - consumer group
  - batch size and batch window
  - retry and error handling policies
  - scaling policies

## Starting Functions with Triggers
- イベント駆動での起動
- 滞留イベントメトリック駆動
- schecule
- webhooks
- resource events

## Maintaining State
- 外部化するしかない

## Functions Calling Other Functions
- Bounded context内でfunctionsとevent streamsをチェーンさせる
- Bounded context内で別functionsを直接呼び出す
  - req/resなら良いけど図のパターンは無しだろ
- orchestration and synchronous function calling
  - orchestratorをfunctionsで作るのはナシだろ
- public cloudのFaaSは1リクエスト＝1インスタンス専有なの触れたほうが良いんじゃないでしょうか


# Chapter 10. Basic Producer and Consumer Microservices
- Basic producer and consumer: 単純なpubsub形式
  - consumer受け取る機能のみ。スケジューリング、ウォーターマーク、チェンジログ機能無し。
  - 軽量で良いと個人的に思うのですが、著者は嫌いらしい。

## Where Do BPCs Work Well?
- with Legacy Systems
- Gating pattern
  - spark streamingとかapache beamで行ける話(FaaSでやる意味)
  - FaaSでやるならState store追記と後続出力は別functionに割りたい

## Hybrid BPC Applications with External Stream Processing
- sparkとかbeamでやれという感想(後の章で出てくるのだろうか)

# 所感
- FaaSにしてもBPCにしても、メリットをもう少し出して欲しいなと思った。
  - qubsubでBPCなら
    - Publisher throughput per region: 12,000,000 kB per minute (200 MB/s) 
    - Pull subscriber throughput per region: 24,000,000 kB per minute (400 MB/s) in large regions
    - Push subscriber throughput per region: 1,200,000 kB per minute (20 MB/s) in large regions
    - StreamingPull subscriber throughput per region: 24,000,000 kB per minute (400 MB/s) in large regions
    - までシャーディング考慮不要で速度出せるのだけれど
