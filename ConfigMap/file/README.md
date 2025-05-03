# 

```bash
k create cm my-index-html --from-file=index.html
configmap/my-index-html created

k run my-index --image=nginx $do > my-index.yaml

vi my-index.yaml 

k apply -f my-index.yaml
pod/my-index created

k get pods
NAME       READY   STATUS    RESTARTS   AGE     IP            NODE     NOMINATED NODE   READINESS GATES
my-index   1/1     Running   0          2m13s   192.168.1.5   node01   <none>           <none>

k run -it --rm --image=curlimages/curl c -- sh
If you don't see a command prompt, try pressing enter.
~ $ curl 192.168.1.5:80
Hello, ConfigMap
```
