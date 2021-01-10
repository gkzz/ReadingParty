## 読書会当日に話したいこと

- chapter 4 よくわからん。。。

## 読書メモ

### Chapter 3. Communication and Data Contracts

* Data contract
  * schema と trigger される timing がある
  * schema 定義することになるよね
  * 互換性もたないと壊れちゃうもんね
* Designing Events
  * Tell the Truth, the Whole Truth, and Nothing but the Truth
  * Use a Singular Event Definition per Stream
  * Use the Narrowest Data Types
  * Keep Events Single-Purpose
  * Minimize the Size of Events
  * Involve Prospective Consumers in the Event Design
  * Avoid Events as Semaphores or Signals

### Chapter 4. Integrating Event-Driven Architectures with Existing Systems

* Data Liberation とはなんなんだろう
  * Event Stream として Event を Subscribe 可能にすること？
* ざっと読んだけどあんまり理解できなかった
  * そんなに手法があるのかもぴんときてない
  * 今まで同期 api を叩いて連携してたものを、event 発行する
  * subscriber はそれを subscribe するようにする、だけでは
  * データの移行が難しいのかな
  * 結果整合になるのはそれはそう
* データ解放パターン
  * Query-based
  * Log-based
  * Table-based
  * よくわからん。。。
