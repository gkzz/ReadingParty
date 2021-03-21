- lineの件
  - [個人情報保護委、LINEに報告求める　法的措置も視野：朝日新聞デジタル](https://www.asahi.com/articles/ASP3M6GC4P3MULZU010.html)
  - [管理不備と報じられたLINEの問題についてまとめてみた - piyolog](https://piyolog.hatenadiary.jp/entry/2021/03/19/072110)

- マスクが届かない
  - [アマゾンでマスク詐欺報告相次ぐ　マーケットプレイスで「商品すり替え」「送料50万円」「届かない」など - ITmedia NEWS](https://www.itmedia.co.jp/news/articles/2003/25/news135.html)

- [git secrets](https://github.com/awslabs/git-secrets)
- [クラウド破産しないように git-secrets を使う - Qiita](https://qiita.com/pottava/items/4c602c97aacf10c058f1)
- https://github.com/Ladicle/kubectl-rolesum
- [Kubeconfigファイルへのサービス・アカウント認証トークンの追加](https://docs.oracle.com/ja-jp/iaas/Content/ContEng/Tasks/contengaddingserviceaccttoken.htm)
- [Workload Identityの実基盤への導入 - Tech Blog - Recruit Lifestyle Engineer](https://engineer.recruit-lifestyle.co.jp/techblog/2019-12-23-workload-identity/)
  - rolebinding -> namespaceレベル
  - clusterrolebinding -> clusterレベル
  ```
  apiVersion: v1
  kind: ServiceAccount
  metadata:
    name: $KSA_NAME
    namespace: $K8S_NAMESPACE   ## <--------これ単位
    annotations:
      iam.gke.io/gcp-service-account:   "$GSA_NAME@$PROJECT_ID.iam.gserviceaccount.com"
  ```

- GKE のアップグレード戦略
  - [Versioning in GKE  |  Kubernetes Engine Documentation  |  Google Cloud](https://cloud.google.com/kubernetes-engine/versioning)
  - [Amazon EKS Kubernetes バージョン - Amazon EKS](https://docs.aws.amazon.com/ja_jp/eks/latest/userguide/kubernetes-versions.html)
  - [リリース チャネル  |  Kubernetes Engine ドキュメント  |  Google Cloud](https://cloud.google.com/kubernetes-engine/docs/concepts/release-channels)
     - > No channel
     - > For more direct management of your cluster's version and nodes, you can choose to not enroll the cluster in a release channel  (that is, no channel) by specifying a static GKE version. Not using a release channel means that you are responsible for managing your  node upgrade strategy. You still must also adhere to the Kubernetes version and version skew support policy, and use supported GKE  versions.
  - [GKE のアップグレード戦略を改めて確認しよう by Yuki Iwanari](https://link.medium.com/oD38BgegNeb)
    - > ■ マスターのアップグレード
    - > 自動アップグレード
    - > 手動アップグレード
    - > ■ ノードのアップグレード
    - > 自動アップグレード
    - > 手動アップグレード（3 パターン）
  - ```
    商用環境 -> no channel
    検証環境 -> stable channel
    問題なければ手動でアップグレード
    ```
  - [Preemptible InstanceでGKEクラスターのオートスケーリング - Ian Lewis](https://www.ianlewis.org/jp/gke-preemptible-instance-autoscaling-ja)

- kubernetesってインフラもアプリも分かっていないと使えない。ロードバランサーはl4/l7どちらでも出てくる。
  - [kubernetesにおけるHTTP/2のロードバランシング](https://qiita.com/immrshc/items/be2e57767bde69b65425)
- CNCFに従わないととなる
  - [物語から入るCloud Nativeな世界(CNCF Cloud Native Landscape編) / CloudNative Days Spring 2021 ONLINE](https://speakerdeck.com/yoshiki0705/cloudnative-days-spring-2021-online?slide=22)
  - > #CNDO2021 で使ったシステム、CloudNative Daysに閉じるつもりはないので、興味のあるカンファレンス主催者の方いましたらお声がけください
    - https://twitter.com/jacopen/status/1370695028725612544?s=20

- Airflow on Kubernetesってどうなの？
  - [【Kubernetes】Airflow on Kubernetesで最強ETL基盤【Airflow】](https://qiita.com/chan-p/items/8d31346dbaa0ee90bccf)