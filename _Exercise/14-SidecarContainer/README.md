# 14-SidecarContainer

## Question

`ambassador`名前空間で稼働している`frontend` Podは、ポート番号8080を使用して、
５秒毎にapi-serviceに接続します。
api-serviceのポート番号は、9090に変更する必要があります。
以下のタスクを実行し、`frontend` Podが引き続き`api-service`に接続できる様に、
新しいコンテナを追加して下さい。

1. `api-service`の公開するポート番号を、`9090`番に変更して下さい
2. `haproxy.cfg`ファイルを使用して、`haproxy-cfg`というConfigMapを作成して下さい。
3. `frontend` Podに、haproxy:alpineイメージを使用したコンテナを追加して下さい。コンテナ名は`haproxy`とし、`/usr/local/etc/haproxy`ディレクトリに`haproxy-cfg` ConfigMapをマウントして下さい。なお、変更には`frontend` Podのマニフェストファイルである`frontend.yaml`を使用して下さい。
4. `frontend`コンテナからServiceへの接続が、新しいエンドポイントに正しくプロキシされる様に、接続先を`api-service`から`localhost`に変更して下さい。

## Answer

```bash
> k get -n ambassador svc
NAME          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
api-service   ClusterIP   10.99.153.165   <none>        8080/TCP   59s

> k edit -n ambassador svc api-service 
service/api-service edited

> k get -n ambassador svc
NAME          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
api-service   ClusterIP   10.99.153.165   <none>        9090/TCP   4m34s

> k create -n ambassador cm haproxy-cfg --from-file=haproxy.cfg 
configmap/haproxy-cfg created

> vi frontend.yaml 

> k apply -f frontend.yaml --force

> k logs -n ambassador frontend --since=15s -c frontend
```