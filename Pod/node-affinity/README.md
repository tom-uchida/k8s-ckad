# node-affinity

```bash
k get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   35d   v1.32.1
node01         Ready    <none>          35d   v1.32.1

k label nodes node01 size=large
node/node01 labeled

vi affinity.yaml

k apply -f affinity.yaml 
pod/affinity created

k get pod -o wide
NAME       READY   STATUS    RESTARTS   AGE   IP            NODE           NOMINATED NODE   READINESS GATES
affinity   1/1     Running   0          48s   192.168.1.6   node01         <none>           <none>
```
