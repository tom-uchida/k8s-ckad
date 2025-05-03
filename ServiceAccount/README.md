# ServiceAccount

```bash
k create sa my-sa
serviceaccount/my-sa created

k create deploy api --image=httpd:alpine --replicas=2
deployment.apps/api created

k set sa deploy api my-sa
deployment.apps/api serviceaccount updated

k describe deploy api | grep my-sa  
  Service Account:  my-sa
```
