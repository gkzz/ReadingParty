# 「Cloud Native DevOps with Kubernetes, 2nd Edition」の4章

Chapter 4. Working with Kubernetes Objects
Deployment
- > Kubernetes has a supervisor feature too: the Deployment
- Dockerでいうsystemdなど
  - cf. https://docs.docker.com/config/daemon/systemd/ 

Deployment v.s. Replicaset
- > ReplicaSetはどんな時でも指定された数のPodのレプリカが稼働することを保証します。しかし、DeploymentはReplicaSetを管理する、より上位レベルの概念で、Deploymentはその他の多くの有益な機能と共に、宣言的なPodのアップデート機能を提供します。
  - Ref. [ReplicaSet | Kubernetes](https://kubernetes.io/ja/docs/concepts/workloads/controllers/replicaset/)