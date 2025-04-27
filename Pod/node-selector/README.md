# node-selector

```bash
k get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   35d   v1.32.1
node01         Ready    <none>          35d   v1.32.1

k label nodes controlplane disktype=ssd
node/controlplane labeled

k run assigned --image=httpd $do > assigned.yaml

vi assigned.yaml 

k apply -f assigned.yaml 
pod/assigned created

k get pod -o wide
NAME       READY   STATUS    RESTARTS   AGE   IP            NODE           NOMINATED NODE   READINESS GATES
assigned   1/1     Running   0          17s   192.168.0.4   controlplane   <none>           <none>
```
