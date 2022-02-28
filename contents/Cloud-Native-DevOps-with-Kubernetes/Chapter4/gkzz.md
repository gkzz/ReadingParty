# 「Cloud Native DevOps with Kubernetes, 2nd Edition」の4章

Chapter 4. Working with Kubernetes Objects

## 深堀したいこと
- 非推奨なマニフェストの書き方の一覧表のようなものはあるのだろうか？
  - 例えば、Replicaset。今はDeploymentを使うことが推奨となっている。 

---
## 読書メモ

Deployment
- > Kubernetes has a supervisor feature too: the Deployment
- Dockerでいうsystemdなど
  - cf. https://docs.docker.com/config/daemon/systemd/ 

Deployment v.s. Replicaset
- DeploymentはReplicaSetを管理し、podはReplicaSetに応じて状態が更新されていく
- > A ReplicaSet ensures that a specified number of pod replicas are running at any given time. However, a Deployment is a higher-level concept that manages ReplicaSets and provides declarative updates to Pods along with a lot of other useful features.
  - Ref. [ReplicaSet | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)
- cf. [Kubernetes道場 8日目 - ReplicaSet / Deploymentについて - Toku's Blog](https://cstoku.dev/posts/2018/k8sdojo-08/)


Podを宣言的な状態へ追随させていくなかで何が起きているのか？、`kube-scheduler` コンポーネントから追うこともできる
- [Kubernetes scheduler visually explained in plain English with a story - azuremonk.com](https://www.azuremonk.com/blog/kube-scheduler)
- [KubernetesのTaintsとTolerationsについて - Qiita](https://qiita.com/sheepland/items/8fedae15e157c102757f)

Service resourcesを使う意義
- podとpodにリクエストを送るクライアントを疎結合とすること
- クライアントはpodに直接アクセスすることはできるが、これではpodが入れ替わるたびにクライアントはpodの名称を知る必要が出てしまう。しかし、podとクライアントが疎結合な関係となると、クライアントはpodが入れ替わったとしてもServiceを介しさえすれば、podにアクセスすることができる。

---
- `reconciliation loop`
  - > Reconciliation loop is part of K8s self healing abilities. 
    - [Kubernetes Self-Healing Reconciliation Loop - DEV Community](https://dev.to/adipolak/kubernetes-self-healing-reconciliation-loop-4aj5)
  - kubernetsの思想を表現する言葉！
  - 宣言的にリソースをマニフェストに定義し、`kubectl apply`コマンドで適用していく