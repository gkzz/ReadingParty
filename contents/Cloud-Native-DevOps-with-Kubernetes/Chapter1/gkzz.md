# 「Cloud Native DevOps with Kubernetes, 2nd Edition」の1章

Chapter 1. Revolution in the Cloud

## 深堀したいこと

- コンピューティングリソースの共同利用はクラウド全盛期の現代にかぎらず1960年代にもみられたというが、当時と現代との違いはなにか？
  - 本書ではDevOpsとクラウド化を挙げている
  - wwwとUnix哲学の広がりも挙げたい
  - cf. [痛快! コンピュータ学 (集英社文庫) | 坂村 健 |本 | 通販 | Amazon](https://www.amazon.co.jp/dp/4087474283)

---
## 読書メモ
- > pay-per-use access to computing resources is a very old idea. Now we call it the cloud, and the revolution that began with timesharing mainframes has come full circle.
  - "クラウド"的な=pay-per-useなコンピューティングリソースの使い方、いわゆるtimesharing mainframesは実は今に始まったことではない。
  - twada氏の「技術選定の審美眼」というスライドを思い出す
  - https://speakerdeck.com/twada/worse-is-better-understanding-the-spiral-of-technologies-2019-edition?slide=10

- 本書でいう3つのレボリューション、Cloud, DevOps, Containersを支えた要因のひとつとして、IaCの進化はあるはず。
  - https://speakerdeck.com/mizzy/infra-study-meetup-number-1?slide=26
  - > 最初はシステム管理の自動化のみが焦点となっていた
  - >  その後（略）ソフトウェア開発のプラクティスをシステム管理に応用するためのもの、と意味合いが変わってきた 

- > Both development teams and operations teams are learning how to work together.
  - TerraformのようないわゆるIaCなツールは両者にとっての共通言語となり、相互理解を促すこと、ひいてはDevOpsの普及に大きく貢献したのではないか？
  - もちろん、本書でいわれているとおりコンテナ化もまたソフトウェアを管理しやすくするという点で貢献しているはず

- > we believe they are destined to become analogous to objects in object-oriented software systems, and as such `will enable the development of distributed system design patterns.`
  - [Design Patterns for Container-based Distributed Systems | USENIX](https://www.usenix.org/conference/hotcloud16/workshop-program/presentation/burns)
  - [コンテナ・デザイン・パターンの論文要約　 - Qiita](https://qiita.com/MahoTakara/items/03fc0afe29379026c1f3)

- > the lack of a standard container orchestration system.
  - コンテナの隆盛とそれがもたらした新たな課題。それを解決すると期待されているのがKubernetes！

- The diffs between orchestration and scheduling
  - > オーケストレーションとは、コンテナー スケジューリング、クラスター管理、および追加ホストのプロビジョニングなども表す広義の用語
  - Ref. [実稼働環境で構成される microservices ベースのアプリケーションを実行する | Microsoft Docs](https://docs.microsoft.com/ja-jp/dotnet/architecture/containerized-lifecycle/run-manage-monitor-docker-environments/run-microservices-based-applications-in-production)

---
- `dawn`
  - noun. the first appearance of light in the sky before sunrise.
  - Syn. daybreak, break of day, crack of dawn, sunrise, first light, daylight

  - `coincidence`
    - n. a remarkable concurrence of events or circumstances without apparent causal connection.
    - Syn. accident, chance, serendipity, fate

- `full circle`
  - n. through a series of developments that lead back to the original source, position, or situation or to a complete reversal of the original position —usually used in the phrase come full circle
  - Ref: https://www.merriam-webster.com/dictionary/full%20circle

- `obsolete`
  - adj. no longer produced or used; out of date.
  - Syn. out of date, outdated, outmoded, old-fashioned

- `occasionally`
  - adv. at infrequent or irregular intervals; now and then.
  - Syn. sometimes, from time to time, (every) now and then, (every) now and again

- `fallacy`
  - n. a mistaken belief, especially one based on unsound arguments.
  - Syn. misconception, mistaken belief, misbelief, delusion

- `frenzy`
  - n. a state or period of uncontrolled excitement or wild behaviour.

- `allocation`
  - n. the action or process of allocating or sharing out something.
  - Syn. allotment, assignment, issuing, issuance, awarding, grant, granting