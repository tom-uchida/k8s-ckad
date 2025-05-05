# 5-Deployment

## Question

Create a redis deployment with the following parameters:

Name of the deployment should be redis using the redis:alpine image.
It should have exactly 1 replica.
The container should request for .2 CPU.
It should use the label app=redis.
It should mount exactly 2 volumes.

a. An Empty directory volume called data at path /redis-master-data.

b. A configmap volume called redis-config at path /redis-master.

c. The container should expose the port 6379.

The configmap has already been created.

## Answer

```bash
k get cm
NAME               DATA   AGE
kube-root-ca.crt   1      42m
redis-config       1      6m39s

k create deploy redis --image=redis:alpine --replicas=1 --dry-run=client -o yaml > redis.yaml

vi redis.yaml

k apply -f redis.yaml
deployment.apps/redis created
```
