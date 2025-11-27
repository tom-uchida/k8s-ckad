# 21-Ingress

## Question

`path-ingress`名前空間では、menu-svcとcontact-svcというClusterIPタイプのServiceが、
それぞれ`menu-app`と`contact-app`というPodを公開しています。
どちらのServiceも、ポート番号は`80`番を使用します。

`contact-svc`は`info-ingress`というIngressによってルーティングされ、
`http://path-ingress.info:31100/contact`を使用して`contact-app`にアクセスすることが出来ます。

`info-ingress`を変更し、`http://path-ingress.info:31100/menu`を使用して
`menu-app`にアクセスできる設定を追加して下さい。

## Answer

```bash
> k get -n path-ingress svc,ingress
NAME                  TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
service/contact-svc   ClusterIP   10.110.76.140   <none>        80/TCP    79s
service/menu-svc      ClusterIP   10.99.198.23    <none>        80/TCP    79s

NAME                                     CLASS   HOSTS               ADDRESS   PORTS   AGE
ingress.networking.k8s.io/info-ingress   nginx   path-ingress.info             80      79s

> curl http://path-ingress.info:31100/contact
Contact

> curl http://path-ingress.info:31100/menu
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx</center>
</body>
</html>

> k edit -n path-ingress ingress info-ingress 
ingress.networking.k8s.io/info-ingress edited

> curl http://path-ingress.info:31100/menu   
Menu
```