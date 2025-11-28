# 23-Service

## Question

`server`名前空間で作成されている`webapp` Podは、nodeコンテナ上で`Express.js`を実行しています。
Podは同じ名前空間に作成されている`websvc` Serviceによって公開される必要があります。

現在、`websvc` Serviceを通じてwebapp Podに接続することができません。
`websvc` Serviceの構成を確認し、問題の原因を修正してください。
なお、変更は`websvc`にのみ適用し、`webapp` Podは変更しないで下さい。

## Answer

```bash
> k get -n server pod,svc
NAME         READY   STATUS    RESTARTS   AGE
pod/webapp   1/1     Running   0          3m22s

NAME             TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
service/websvc   NodePort   10.97.214.184   <none>        80:30500/TCP   3m22s

> curl controlplane:30500
curl: (7) Failed to connect to controlplane port 30500 after 2 ms: Couldn't connect to server

> k describe -n server svc websvc 
Name:                     websvc
Namespace:                server
Labels:                   run=webapp
Annotations:              <none>
Selector:                 run=webapp
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.97.214.184
IPs:                      10.97.214.184
Port:                     <unset>  80/TCP
TargetPort:               3000/TCP
NodePort:                 <unset>  30500/TCP
Endpoints:                192.168.1.4:3000
Session Affinity:         None
External Traffic Policy:  Cluster
Internal Traffic Policy:  Cluster
Events:                   <none>

> k describe -n server pod webapp | grep PORT
      PORT:  3030

> k edit -n server svc websvc 
service/websvc edited

> curl controlplane:30500
<!DOCTYPE html><html><head><title>Express</title><link rel="stylesheet" href="/stylesheets/style.css"></head><body><h1>Express</h1><p>Welcome to Express</p></body></html>
```