# 4-Deployment

## Question

Create a new deployment called nginx-deploy, with one single container called nginx, image nginx:1.16 and 4 replicas.
The deployment should use RollingUpdate strategy with maxSurge=1, and maxUnavailable=2.

Next upgrade the deployment to version 1.17.

Finally, once all pods are updated, undo the update and go back to the previous version.

## Answer

```bash
k create deploy nginx-deploy --image=nginx:1.16 --replicas=4 --dry-run=client -o yaml > nginx-deploy.yaml

vi nginx-deploy.yaml

k apply -f nginx-deploy.yaml
deployment.apps/nginx-deploy created

k set image  deployment nginx-deploy nginx=nginx:1.17
deployment.apps/nginx-deploy image updated

k get deploy
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deploy   4/4     4            4           2m57s

k rollout undo deployment nginx-deploy 
deployment.apps/nginx-deploy rolled back

k get deploy
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deploy   2/4     3            2           3m23s
```
