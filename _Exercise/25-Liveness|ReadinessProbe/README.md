# 25-Liveness|ReadinessProbe

## Question

`probes`名前空間では、`web`という名前のPodが作成されています。
`web` PodにHTTPリクエストによるLiveness ProbeとReadiness Probeを追加して下さい。
詳細は以下のとおりです。

Liveness Probeでは、`80`番ポートを使用して`/live`エンドポイントが正常なステータスコードを返すかどうかを認識します。
最初のProbeを実行する前に`5`秒間待機し、その後、`10秒`おきに実行されます。

Readiness Probeでは、`80`番ポートを使用して`/ready`エンドポイントが正常なステータスコードを返すかどうかを認識します。
最初のProbeを実行する前に`15`秒間待機し、その後、`10`秒おきに実行されます。

ダウンロードした`web.yaml`は、`web` Podのマニフェストファイルです。
上記のLiveness ProbeとReadiness Probeを`web.yaml`に追加し、実行中のPodに変更を適用して下さい。

## Answer

```bash
> vi web.yaml 

> k replace -f web.yaml --force
pod/web replaced

> k describe -n probes pod web | grep Liveness
    Liveness:       http-get http://:80/live delay=5s timeout=1s period=10s #success=1 #failure=3

> k describe -n probes pod web | grep Readiness
    Readiness:      http-get http://:80/ready delay=15s timeout=1s period=10s #success=1 #failure=3
```