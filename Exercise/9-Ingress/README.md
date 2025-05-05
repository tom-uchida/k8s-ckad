# 9-Ingress

## Question

Create a single ingress resource called ingress-vh-routing.
The resource should route HTTP traffic to multiple hostnames as specified below:

- The service video-service should be accessible on http://watch.ecom-store.com:30093/video
- The service apparels-service should be accessible on http://apparels.ecom-store.com:30093/wear

To ensure that the path is correctly rewritten for the backend service, add the following annotation to the resource:
nginx.ingress.kubernetes.io/rewrite-target: /

Here 30093 is the port used by the Ingress Controller

## Answer

```bash
k get svc
NAME               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
apparels-service   ClusterIP   172.20.128.47    <none>        8080/TCP   7m43s
kubernetes         ClusterIP   172.20.0.1       <none>        443/TCP    54m
video-service      ClusterIP   172.20.174.105   <none>        8080/TCP   7m43s

vi ingress.yaml

k apply -f ingress.yaml 
ingress.networking.k8s.io/ingress-vh-routing created

k get ingress
NAME                 CLASS    HOSTS                                          ADDRESS   PORTS   AGE
ingress-vh-routing   <none>   watch.ecom-store.com,apparels.ecom-store.com             80      5s
```
