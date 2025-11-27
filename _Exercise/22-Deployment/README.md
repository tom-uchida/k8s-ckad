# 22-Deployment

## Question

`pay`名前空間では、`payment` Deploymentが`payment-svc`というServiceにより、
NodePort番号`31120`を使用して外部のネットワークに公開されています。

カナリアデプロイメント戦略を利用し、アプリケーションの新しいバージョンをリリースする必要があります。
以下のタスクを実行し、新しいバージョンをDeploymentで作成されるレプリカの20％に展開して下さい。
また、アプリケーションを実行するレプリカ数の合計は`5`に設定して下さい。

1. `payment`と同じPodの構成で、`payment-canary` というDeploymentを作成して下さい。`app-version`ラベルの値には、`canary`を設定して下さい。レプリカ数には、アプリケーションを実行する合計の`20％`を設定して下さい。（`payment.yaml`は、`payment` Deploymentのマニフェストです。ファイルをコピーして`payment-canary` Deploymentの作成に使用して下さい。）
2. `payment-svc`を更新し、トラフィックの`20％`を`payment-canary`に送信して下さい。

なお、`curl controlplane:31120`を実行することで`payment-svc`への接続をテストする事が出来ます。

## Answer

```bash
> k get -n pay deploy,svc
NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/payment   3/3     3            3           74s

NAME                  TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
service/payment-svc   NodePort   10.98.98.155   <none>        80:31120/TCP   74s

> cp payment.yaml payment-canary.yaml 

> vi payment-canary.yaml 

> k apply -f payment-canary.yaml 
deployment.apps/payment-canary created

> k get -n pay deploy
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
payment          3/3     3            3           6m52s
payment-canary   1/1     1            1           30s

> k scale -n pay deploy payment --replicas=4
deployment.apps/payment scaled

> k get -n pay deploy
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
payment          4/4     4            4           7m41s
payment-canary   1/1     1            1           79s

> k edit -n pay svc payment-svc 
service/payment-svc edited

> curl controlplane:31120
app="payment"
app-version="canary"
pod-template-hash="7fbf6bdb95"

> curl controlplane:31120
app="payment"
app-version="stable"
pod-template-hash="ccc665c74"

> curl controlplane:31120
app="payment"
app-version="stable"
pod-template-hash="ccc665c74"

> curl controlplane:31120
app="payment"
app-version="stable"
pod-template-hash="ccc665c74"

> curl controlplane:31120
app="payment"
app-version="stable"
```