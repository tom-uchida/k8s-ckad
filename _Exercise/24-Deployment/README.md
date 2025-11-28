# 24-Deployment

## Question

1. `rolling-update`という名前空間を作成し、`rolling`という名前のDeploymentを作成して下さい。イメージは`redis:6.2-alpine`を使用し、レプリカ数は`5`とします。strategyのtypeには`RollingUpdate`を指定し、maxSurgeを`20%`、maxUnavailableを`2`に設定して下さい。
2. `kubectl set`コマンドを実行し、`rolling` Deploymentが実行するコンテナのイメージを`redis:7.2-alpine`に更新して下さい。
3. `rolling` Deploymentを一つ前のリビジョンにロールバックして下さい。

## Answer

```bash
> k create ns rolling-update
namespace/rolling-update created

> k create -n rolling-update deploy rolling --image=redis:6.2-alpine --replicas=5 --dry-run=client -oyaml > rolling.yaml

> vi rolling.yaml 

> k apply -f rolling.yaml 
deployment.apps/rolling created

> k get -n rolling-update deployments.apps -owide
NAME      READY   UP-TO-DATE   AVAILABLE   AGE    CONTAINERS   IMAGES             SELECTOR
rolling   5/5     5            5           6m6s   redis        redis:6.2-alpine   app=rolling

> k set -n rolling-update image deploy rolling redis=redis:7.2-alpine
deployment.apps/rolling image updated

> k get -n rolling-update deployments.apps -owide
NAME      READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES             SELECTOR
rolling   5/5     5            5           6m36s   redis        redis:7.2-alpine   app=rolling

> k rollout -n rolling-update undo deployment rolling 
deployment.apps/rolling rolled back

> k get -n rolling-update deployments.apps -owide
NAME      READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES             SELECTOR
rolling   5/5     5            5           6m59s   redis        redis:6.2-alpine   app=rolling
```