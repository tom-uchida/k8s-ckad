# 16-NetworkPolicy

## Question

`network`名前空間では、デフォルトでは全てのPodの内向き（ingress）トラフィックが無効化されています。
`web` Podからapi Podへの内向きのトラフィックを許可するため、`api-netpol`というNetworkPolicyが作成されましたが、エラーが発生しています。
`web` Podに必要な設定を追加し、`api` Podへの接続を有効化して下さい。

なお、解答に必要なKubernetesリソースは全て作成されており、新しく作成する必要はありません。
また、既存のNetworkPolicyは変更または削除しないでください。

## Answer

```bash
> k get pod -n network -o wide        
NAME   READY   STATUS    RESTARTS   AGE   IP            NODE     NOMINATED NODE   READINESS GATES
api    1/1     Running   0          11m   192.168.1.5   node01   <none>           <none>
web    1/1     Running   0          11m   192.168.1.4   node01   <none>           <none>

> k exec -n network web -- sh -c "curl -m 2 192.168.1.5"
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:--  0:00:02 --:--:--     0
curl: (28) Connection timed out after 2002 milliseconds
command terminated with exit code 28

> k get netpol -n network api-netpol -oyaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"networking.k8s.io/v1","kind":"NetworkPolicy","metadata":{"annotations":{},"name":"api-netpol","namespace":"network"},"spec":{"ingress":[{"from":[{"podSelector":{"matchLabels":{"role":"backend"}}}],"ports":[{"port":80,"protocol":"TCP"}]}],"podSelector":{"matchLabels":{"role":"api"}},"policyTypes":["Ingress"]}}
  creationTimestamp: "2025-11-24T12:42:17Z"
  generation: 1
  name: api-netpol
  namespace: network
  resourceVersion: "3065"
  uid: b335c9a5-513e-4092-8b46-19f8397ed48f
spec:
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: backend
    ports:
    - port: 80
      protocol: TCP
  podSelector:
    matchLabels:
      role: api
  policyTypes:
  - Ingress

> k get pod -n network  --show-labels 
NAME   READY   STATUS    RESTARTS   AGE   LABELS
api    1/1     Running   0          15m   role=api
web    1/1     Running   0          15m   app=web

> k label -n network pod web role=backend
pod/web labeled

> k exec -n network web -- sh -c "curl -m 2 192.168.1.5"
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0Welcome to api!
100    16  100    16    0     0   7629      0 --:--:-- --:--:-- --:--:--  8000
```