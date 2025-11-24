# 15-ServiceAccount

## Question

`service`名前空間で実行される`pod-reader` Deploymentは、5秒ごとに"kubectl get pods"コマンドを実行します。

現在、Deploymentのログにはエラーメッセージが出力されています。
以下のタスクを実行し、エラーを修正して下さい。
なお、解答に必要なリソースは全て作成されており、新しいリソースを作成する必要はありません。

1. `pod-reader` Deploymentのログを確認し、エラーメッセージを調査して下さい。
2. `pod-reader` Deploymentを修正し、エラーの原因となっている問題を解決して下さい。

## Answer

```bash
> k logs -n service deployments/pod-reader --since=5s
Error from server (Forbidden): pods is forbidden: User "system:serviceaccount:service:default" cannot list resource "pods" in API group "" in the namespace "service"

> k auth -n service can-i list pods --as=system:serviceaccount:service:default      
no

> k auth -n service can-i list pods --as=system:serviceaccount:service:pod-reader-sa
yes

> k set sa deploy -n service pod-reader pod-reader-sa
deployment.apps/pod-reader serviceaccount updated

> k rollout restart -n service deployment pod-reader 
deployment.apps/pod-reader restarted
```