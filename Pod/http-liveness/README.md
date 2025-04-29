# http-liveness

```bash
k run http-liveness --image=nginx $do > http-liveness.yaml

vi http-liveness.yaml

k apply -f http-liveness.yaml 
pod/http-liveness created

k get pod
NAME            READY   STATUS    RESTARTS   AGE
http-liveness   1/1     Running   0          104s
```
