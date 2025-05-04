# NetworkPolicy

```bash
k apply -f https://raw.githubusercontent.com/nz-cloud-udemy/ckad-questions/main/service-and-networking/netpol/resources.yaml
namespace/backend created
pod/web1 created
pod/web2 created
pod/web3 created
networkpolicy.networking.k8s.io/default-deny-all created

k config set-context --current --namespace backend
Context "kubernetes-admin@kubernetes" modified.

k get pods -o wide
NAME   READY   STATUS    RESTARTS   AGE    IP             NODE     NOMINATED NODE   READINESS GATES
web1   1/1     Running   0          2m2s   192.168.1.8    node01   <none>           <none>
web2   1/1     Running   0          2m2s   192.168.1.9    node01   <none>           <none>
web3   1/1     Running   0          2m2s   192.168.1.10   node01   <none>           <none>

export web1=192.168.1.8 
export web2=192.168.1.9
export web3=192.168.1.10

k exec web1 -- sh -c "curl -s -m 2 $web2"
Defaulted container "web1" out of: web1, init-con (init)
command terminated with exit code 28

k exec web1 -- sh -c "curl -s -m 2 $web3"
Defaulted container "web1" out of: web1, init-con (init)
command terminated with exit code 28

k exec web2 -- sh -c "curl -s -m 2 $web1"
Defaulted container "web2" out of: web2, init-con (init)
command terminated with exit code 28

k exec web2 -- sh -c "curl -s -m 2 $web3"
Defaulted container "web2" out of: web2, init-con (init)
command terminated with exit code 28

k exec web3 -- sh -c "curl -s -m 2 $web1"
Defaulted container "web3" out of: web3, init-con (init)
command terminated with exit code 28

k exec web3 -- sh -c "curl -s -m 2 $web2"
Defaulted container "web3" out of: web3, init-con (init)
command terminated with exit code 28

vi web1-netpol.yaml
cp web1-netpol.yaml web3-netpol.yaml
vi web3-netpol.yaml 

k apply -f web1-netpol.yaml 
networkpolicy.networking.k8s.io/web1-netpol created
k apply -f web3-netpol.yaml 
networkpolicy.networking.k8s.io/web3-netpol created

k exec web1 -- sh -c "curl -s -m 2 $web3"
Defaulted container "web1" out of: web1, init-con (init)
web3

k exec web1 -- sh -c "curl -s -m 2 $web2"
Defaulted container "web1" out of: web1, init-con (init)
command terminated with exit code 28

k exec web3 -- sh -c "curl -s -m 2 $web1"
Defaulted container "web3" out of: web3, init-con (init)
web1

k exec web3 -- sh -c "curl -s -m 2 $web2"
Defaulted container "web3" out of: web3, init-con (init)
command terminated with exit code 28

k exec web2 -- sh -c "curl -s -m 2 $web1"
Defaulted container "web2" out of: web2, init-con (init)
command terminated with exit code 28

k exec web2 -- sh -c "curl -s -m 2 $web3"
Defaulted container "web2" out of: web2, init-con (init)
command terminated with exit code 28
```
