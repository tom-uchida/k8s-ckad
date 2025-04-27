# blue-green

```bash
wget https://raw.githubusercontent.com/nz-cloud-udemy/ckad-questions/main/application-deployment/blue-green-deployment/blue.yaml
2025-04-27 13:21:46 (12.4 MB/s) - 'blue.yaml' saved [679/679]

kubectl apply -f https://raw.githubusercontent.com/nz-cloud-udemy/ckad-questions/main/application-deployment/blue-green-deployment/resources.yaml
namespace/bgd created
deployment.apps/blue created
service/blue-green-svc created

curl controlplane:31230
app-version="blue"
pod-template-hash="575d986bd9"
product="my-web-app"

cp blue.yaml green.yaml
vi green.yaml

k apply -f green.yaml 
deployment.apps/green created

k get deployment -n bgd
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
blue    3/3     3            3           5m21s
green   3/3     3            3           2m17s

k edit svc -n bgd blue-green-svc 
service/blue-green-svc edited

curl controlplane:31230
app-version="green"
pod-template-hash="5c7b8494cb"
product="my-web-app"
```
