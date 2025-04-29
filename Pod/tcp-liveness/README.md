# tcp-liveness

```bash
k run tcp-liveness --image=goproxy/goproxy --port=8080 $do > tcp-liveness.yaml

vi tcp-liveness.yaml

k apply -f tcp-liveness.yaml
pod/tcp-liveness created

k get pods
tcp-liveness    1/1     Running   0          22s
```
