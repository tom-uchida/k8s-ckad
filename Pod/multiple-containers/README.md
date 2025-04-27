# multiple-containers

```bash
k run multiple --image=httpd $do > multiple.yaml

vi multiple.yaml

k apply -f multiple.yaml
pod/multiple created

k get pod
NAME       READY   STATUS    RESTARTS   AGE
multiple   2/2     Running   0          11s

k exec multiple -c secondary -- sh -c "wget -qO- http://localhost"
<html><body><h1>It works!</h1></body></html>
```
