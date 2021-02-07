## 読書メモ

# Chapter9
- Ensure Strict Membership to a Bounded Context
  - Ensure that data stores are kept private from external contexts.
    →external contextsに対してそうなのはわかるが、その理屈では上流に対してもそうすべきでは？
- Less Is More
  - それはそう。
- OpenWhisk, OpenFaaS, Nuclio, and Kubeless
  - 日本で使っている事例って？
- Building Microservices Out of Functions
  - The function
  - Input event stream
  - Triggering logic
  - Error and scaling policies, with metadata

# GCPのこれは、AWSのStep Functionsに相当するものですかね？
- [Google Cloudのサーバレスワークフローサービス、WorkflowsがGAに](https://cloud.google.com/workflows/docs/connectors)
  - 同時にFirestoreやPub/Subなどへのコネクタがプレビューとなり、よりこれらのサービスを利用したワークフロー処理を書きやすくなりました。