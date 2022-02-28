# 「Cloud Native DevOps with Kubernetes, 2nd Edition」の3章

Chapter 3. Getting Kubernetes

## 深堀したいこと

なし

---
## 読書メモ

![image](https://user-images.githubusercontent.com/38461277/155911031-c223b007-e67d-4a6e-a95e-6842c8f4b03e.png)
Ref. [How Kubernetes works | Cloud Native Computing Foundation](https://www.cncf.io/blog/2019/08/19/how-kubernetes-works/)
- 用語集
  - [Kubernetes Components | Kubernetes](https://kubernetes.io/docs/concepts/overview/components/)
    - > The worker node(s) host the Pods that are the components of the application workload. `The control plane manages the worker nodes and the Pods in the cluster.`  

- The Costs of Self-Hosting Kubernetes
  - マネージド Kubernetesサービスが好まれる理由
  - セルフホストはたしかにデプロイするだけでKubernetesを起動することはできる。ただし、Kubernetesを運用するところまで踏み込むと考えることがたくさん、、！
    - コントロールプレーンの耐障害性は考慮されているか？(コントロールプレーンのアップデート作業時間、ダウンタイムはどこまで許容されるように設計するか？)
    - クラスター間の内部通信はセキュア？
    - etcdは適切に管理されている？
    - Kubernetesの下層レイヤーに位置するOSレベル、カーネルらのアップデート対応は追随できる？


- Run Less Software
  - > - Choose standard technology
    > - Outsource undifferentiated heavy lifting
    > - Create enduring competitive advantage 
---
- `intrinsic`
  - adj. belonging naturally; essential.
- `conformant`  
  - adj. (especially of technology) compatible or conforming with appropriate standards.
  - e.g. "vendors are using the test tool and expect to announce conformant products soon"