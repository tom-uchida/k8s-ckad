# init-containers

```bash
k run init-pod --image=nginx:alpine $do > init-pod.yaml

vi init-pod.yaml

k apply -f init-pod.yaml 
pod/init-pod created

k get pods -o wide
NAME       READY   STATUS    RESTARTS   AGE   IP            NODE     NOMINATED NODE   READINESS GATES
init-pod   1/1     Running   0          61s   192.168.1.6   node01   <none>           <none>

k run -it --rm --image=curlimages/curl c -- sh
If you don't see a command prompt, try pressing enter.
~ $ curl 192.168.1.6
Hello, World!
```
