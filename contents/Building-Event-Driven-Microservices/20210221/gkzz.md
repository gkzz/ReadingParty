# 「Building Event-Driven Microservices」の13章
2021/02/21(Sun) 09:00am-10:30am

## 読書会当日に話したいこと
### Chapter 13. Integrating Event-Driven and Request-Response Microservices
Figure13-8, 13-9の2つの結合のカタチがあることはたしかにあると感じた。後者のほうがよいけどデメリットとしてサービス間で変更することは大変であること。

- Figure 13-8. An all-in-one microservice serving from external state store; note that either instance could serve the request
- Figure 13-9. A microservice composed of separate executables—one for serving requests, the other for processing events
  - **`CAUTION`**
    - 2つのマイクロサービスはひとつとしてデプロイされる
    -  >  While this pattern has two microservices operating on a single data store, there’s still just a single bounded context. `These two microservices are treated as a single composite service. They reside within the same code repository and are tested, built, and deployed together.`
  - デメリット
    - > Coordinating changes between two otherwise independent applications is risky, as altering the data structures, topologies, and request patterns can necessitate dependent changes in both services.  

---

## 読書メモ

### Chapter 13. Integrating Event-Driven and Request-Response Microservices
#### Two main types of externally generated events to consider.
  - > Autonomously Generated Events 
    - be sent from client to server autonomously by your products
    - be defined as a metric or measurement from the product
    - e.g.: information about what a user is doing, periodic measurements of activity, or sensor readings of some sort.
    - Netflixが利用者が視聴した動画視聴履歴を収集すること
  - > Reactively Generated Events
    - [Chatwork、LINE、Netflixが進めるリアクティブシステムとは？　メリットは？　実現するためのライブラリは？：リアクティブプログラミング超入門（1）（1/2 ページ） - ＠IT](https://www.atmarkit.co.jp/ait/articles/1703/16/news023.html)
    - [リアクティブマイクロサービス入門（1/2）- 概念編 - Qiita](https://qiita.com/crossroad0201/items/7c8892c459ecef39ccef)
      - > ユーザーにとって直接的に価値があるのは「即応性」 であり、それを常に保つために「耐障害性」「弾力性」が必要であり、それらは「メッセージ駆動」を基盤とすることで実現される 
    - https://gihyo.jp/assets/images/design/serial/01/ad-and-tech/0004/05.png
    - [第4回　インターネット広告配信と測定の仕組み：インターネット広告とテクノロジーの行方｜gihyo.jp … 技術評論社](https://gihyo.jp/design/serial/01/ad-and-tech/0004?page=3)

- Figure 13-3. Integrating request-response APIs into event-driven workflows

#### Serving Real-Time Requests with External State Stores
- > Ensure that `state is accessed via the request-response API of the microservice and not through a direct coupling with the state store.` Failure to do so introduces a shared data store, resulting in tight coupling between services, and makes changes difficult and risky.

- cf. [外部構成ストア パターン - Cloud Design Patterns | Microsoft Docs](https://docs.microsoft.com/ja-jp/azure/architecture/patterns/external-configuration-store)

#### Micro-Frontends in Request-Response Applications
- match up very well with event-driven microservice backends
- Pros:
  - modularity
  -  separation of business concerns, autonomous teams, and deployment, language, and code-base independence.
  - Figure 13-14. Three main approaches to organizing products and teams for customer-facing content
  - Figure 13-15. Experiences search and review application, GUI mockup version 1 with monolithic frontend
  - cf. [マイクロサービスを基にしている複合 UI を作成する | Microsoft Docs](https://docs.microsoft.com/ja-jp/dotnet/architecture/microservices/architect-microservice-container-applications/microservice-based-composite-ui-shape-layout)

- Cons
  -  potential for duplicated code and the operational concerns of managing and deploying microservices
  - マイクロサービスで言われていた点と同じ

- 以前の読書会でもMicro-Frontendsは扱っていた
  - https://github.com/gkzz/ReadingParty/blob/main/contents/Fundamentals-of-Software-Architecture/20201227/hackmd.md
  - [[翻訳記事]マイクロフロントエンド マイクロサービスのフロントエンドへの応用](https://micro-frontends-japanese.org/)

----
- `cease`
  - verb
  - meaning: come or bring to an end.
    - Syn: come to an end 
   
- `await`
  - > The other difference between the two verbs, 'wait' and 'await', is the level of formality. 'Await' is more formal than 'wait' - it would be used in formal letters, for example.
    - Source: [BBC World Service | Learning English | Ask about English](https://www.bbc.co.uk/worldservice/learningenglish/radio/specials/1535_questionanswer/page15.shtml) 
   
- `precedence`
  - noun
  - meaning: the condition of being considered more important than someone or something else; priority in importance, order, or rank.
 
- `predominantly`
  - adv
    - meaning: mainly; for the most part. 

- `autonomous`
  - noun
  - meaning: a person or entity that is self-controlling and not governed by outside forces.  

- `adhere`
  - verb
  - meaning: stick fast to (a surface or substance).
  - Syn: stick, stick fast, cling, hold fast, cohere, bond, attach

- `encapsulation`
  - カプセル化
  - > In object-oriented programming (OOP), encapsulation refers to the bundling of data with the methods that operate on that data, or the restricting of direct access to some of an object's components.[1] Encapsulation is used `to hide the values or state of a structured data object inside a class, preventing direct access` to them by clients in a way that could expose hidden implementation details or violate state invariance maintained by the methods.
  - Source: [Encapsulation (computer programming) - Wikipedia](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming))
