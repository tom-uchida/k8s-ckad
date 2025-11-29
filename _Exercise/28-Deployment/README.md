# 28-Deployment

## Question

`session`名前空間では、`redis-deploy`という名前のDeploymentが作成されています。
このDeploymentは、`redis:alpine`イメージを使用したコンテナをレプリカ数1で実行することを目的としていますが、
現在エラーが発生しており、Podの起動に失敗しています。
エラーの原因を特定し、問題を解決して下さい。

## Answer

```bash
> k get pod -n session 
NAME                            READY   STATUS             RESTARTS   AGE
redis-deploy-6cbdfb5b67-lpftm   0/1     ImagePullBackOff   0          9m

> k describe pod -n session | grep not      
Annotations:      cni.projectcalico.org/containerID: 081312e14efd17857d7e94452d38f166f65243208b82dbe856dc6b8732cd969d
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
  Warning  Failed     7m42s (x5 over 10m)  kubelet            Failed to pull image "redis:alpinee": rpc error: code = NotFound desc = failed to pull and unpack image "docker.io/library/redis:alpinee": failed to resolve reference "docker.io/library/redis:alpinee": docker.io/library/redis:alpinee: not found

> k get pod,deploy -n session 
NAME                              READY   STATUS    RESTARTS   AGE
pod/redis-deploy-b6c7f9f4-pwwmg   1/1     Running   0          92s

NAME                           READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/redis-deploy   1/1     1            1           13m
```