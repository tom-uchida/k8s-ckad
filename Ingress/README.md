# Ingress

```bash
curl -s https://raw.githubusercontent.com/nz-cloud-udemy/ckad-questions/main/service-and-networking/ingress/init-ingress.sh | sh
Release "ingress-nginx" does not exist. Installing it now.
NAME: ingress-nginx
LAST DEPLOYED: Sun May  4 07:21:25 2025
NAMESPACE: ingress-nginx
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
The ingress-nginx controller has been installed.
It may take a few minutes for the load balancer IP to be available.
You can watch the status by running 'kubectl get service --namespace ingress-nginx ingress-nginx-controller --output wide --watch'

An example Ingress that makes use of the controller:
  apiVersion: networking.k8s.io/v1
  kind: Ingress
  metadata:
    name: example
    namespace: foo
  spec:
    ingressClassName: nginx
    rules:
      - host: www.example.com
        http:
          paths:
            - pathType: Prefix
              backend:
                service:
                  name: exampleService
                  port:
                    number: 80
              path: /
    # This section is only required if TLS is to be enabled for the Ingress
    tls:
      - hosts:
        - www.example.com
        secretName: example-tls

If TLS is enabled for the Ingress, a Secret containing the certificate and key must also be provided:

  apiVersion: v1
  kind: Secret
  metadata:
    name: example-tls
    namespace: foo
  data:
    tls.crt: <base64 encoded cert>
    tls.key: <base64 encoded key>
  type: kubernetes.io/tls

k apply -f https://raw.githubusercontent.com/nz-cloud-udemy/ckad-questions/main/service-and-networking/ingress/resources.yaml
configmap/default-config created
pod/hello-app created
service/hello-svc created
service/ingress-nginx-controller-service created

k get all
NAME            READY   STATUS    RESTARTS   AGE
pod/hello-app   1/1     Running   0          9s

NAME                 TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
service/hello-svc    ClusterIP   10.99.72.252   <none>        80/TCP    9s
service/kubernetes   ClusterIP   10.96.0.1      <none>        443/TCP   5d19h

k create ingress hello-ingress --class=nginx --rule="hello-ckad.example/=hello-svc:80"
ingress.networking.k8s.io/hello-ingress created

curl hello-ckad.example:30100
Hello CKAD!
```
