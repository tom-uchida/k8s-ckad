# 20-SecurityContext

## Question

`context`という名前空間を作成し、そこにsecure-redisというPodを作成して下さい。
コンテナイメージには、`redis:alpine`を使用し、コンテナのSecurityContextには以下の項目を設定して下さい。

- ユーザーID: `2000`で実行する。
- Privilege escalationを`true`とする。
- `NET_ADMIN` capabilityを付与する。

## Answer

```bash
> k create ns context
namespace/context created

> k run secure-redis -n context --image=redis:alpine --dry-run=client -oyaml > secure-redis.yaml

> vi secure-redis.yaml

> k apply -f secure-redis.yaml 
pod/secure-redis created

> k get -n context pod secure-redis -o jsonpath="{.spec.containers[0].securityContext}"
{"allowPrivilegeEscalation":true,"capabilities":{"add":["NET_ADMIN"]},"runAsUser":2000}
```