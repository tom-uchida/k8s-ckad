# 12-Secret

## Question

`credential`名前空間で、login Deploymentが実行するコンテナは環境変数`USERNAME`と`PASSWORD`を`creds` Secretから参照しています。
`creds`が保持している`PASSWORD`の値を`my-new-password`に変更して下さい。

## Answer

```bash
> k exec -it -n credential deployments/login -- env | grep PASSWORD
PASSWORD=my-current-password

> k get -n credential secret
NAME    TYPE     DATA   AGE
creds   Opaque   2      7m24s

> echo "my-new-password" | base64   
bXktbmV3LXBhc3N3b3JkCg==

> k edit -n credential secret creds 
secret/creds edited

> k rollout restart -n credential deployment login 
deployment.apps/login restarted

> k exec -it -n credential deployments/login -- env | grep PASSWORD
PASSWORD=my-new-password
```