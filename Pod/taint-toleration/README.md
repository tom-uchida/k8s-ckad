# taint-toleration

```bash
k get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   35d   v1.32.1
node01         Ready    <none>          35d   v1.32.1

k taint nodes node01 dedicated=admin:NoSchedule
node/node01 tainted

k run admindb --image=redis:alpine $do > admindb.yaml

vi admindb.yaml

k apply -f admindb.yaml 
pod/admindb created

k get pod -o wide
NAME       READY   STATUS    RESTARTS   AGE   IP            NODE           NOMINATED NODE   READINESS GATES
admindb    1/1     Running   0          8s    192.168.1.7   node01         <none>           <none>
```
