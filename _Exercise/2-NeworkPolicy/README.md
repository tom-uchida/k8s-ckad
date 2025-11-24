# 2-NetworkPolicy

## Question

We have deployed a new pod called secure-pod and a service called secure-service.
Incoming or Outgoing connections to this pod are not working.
Troubleshoot why this is happening.

Make sure that incoming connection from the pod webapp-color are successful.

Important: Don't delete any current objects deployed.

## Answer

```bash
k get pods
NAME           READY   STATUS    RESTARTS   AGE
logger         1/1     Running   0          2m5s
secure-pod     1/1     Running   0          39s
webapp-color   1/1     Running   0          9m55s

k get svc
NAME             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
kubernetes       ClusterIP   172.20.0.1       <none>        443/TCP   29m
secure-service   ClusterIP   172.20.246.126   <none>        80/TCP    77s

k get netpol
NAME           POD-SELECTOR   AGE
default-deny   <none>         2m41s

k describe netpol default-deny 
Name:         default-deny
Namespace:    default
Created on:   2025-05-04 14:02:09 +0000 UTC
Labels:       <none>
Annotations:  <none>
Spec:
  PodSelector:     <none> (Allowing the specific traffic to all pods in this namespace)
  Allowing ingress traffic:
    <none> (Selected pods are isolated for ingress connectivity)
  Not affecting egress traffic
  Policy Types: Ingress

k get pods --show-labels
NAME           READY   STATUS    RESTARTS   AGE     LABELS
logger         1/1     Running   0          6m29s   <none>
secure-pod     1/1     Running   0          5m3s    run=secure-pod
webapp-color   1/1     Running   0          14m     name=webapp-color

k get netpol dfault-deny -o yaml > netpol.yaml

vi netpol.yaml

k apply -f netpol.yaml
networkpolicy.networking.k8s.io/network-policy created
```
