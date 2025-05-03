# Secret

```bash
k create secret generic db-secret --from-literal=DB_HOST=127.0.0.1 --from-literal=DB_PASSWORD=changeit
secret/db-secret created

k run redis-pod --image=redis $do > redis-pod.yaml

vi redis-pod.yaml 

k apply -f redis-pod.yaml 
pod/redis-pod created

k get pods
NAME        READY   STATUS    RESTARTS   AGE
redis-pod   1/1     Running   0          9s

k exec -it redis-pod -- env
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=redis-pod
GOSU_VERSION=1.17
REDIS_VERSION=7.4.3
REDIS_DOWNLOAD_URL=http://download.redis.io/releases/redis-7.4.3.tar.gz
REDIS_DOWNLOAD_SHA=e1807d7c0f824f4c5450244ef50c1e596b8d09b35d03a83f4e018fb7316acf45
REDIS_HOST=127.0.0.1
REDIS_PASSWORD=changeit
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT=tcp://10.96.0.1:443
KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_PORT_443_TCP_PORT=443
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
KUBERNETES_SERVICE_HOST=10.96.0.1
KUBERNETES_SERVICE_PORT=443
TERM=xterm
HOME=/root
```
