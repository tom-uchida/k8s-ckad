# cluster-ip

```bash
k create deploy httpd-deploy --image=httpd:alpine --replicas=2
deployment.apps/httpd-deploy created

k expose deploy httpd-deploy --name=httpd-svc --type=ClusterIP --port=80
service/httpd-svc exposed

k run -it --rm --image=curlimages/curl c -- sh
If you don't see a command prompt, try pressing enter.
~ $ curl httpd-svc
<html><body><h1>It works!</h1></body></html>
```
