# 26-Helm

## Question

1. helmに`bitnami`という名前のリポジトリを追加して下さい。リポジトリのURLは`https://charts.bitnami.com/bitnami`を使用して下さい。
2. `helm search repo`コマンドを使用して`bitnami/nginx`チャートが存在することを確認して下さい。
3. helmを使用して`ckad-helm`名前空間に`bitnami/nginx`チャートをインストールして下さい。リリース名は`my-nginx`とします。
4. `helm list`コマンドを実行して、`my-nginx`がデプロイされていることを確認後、`kubectl get deploy` コマンドを実行して、レプリカの数を確認して下さい。
5. `helm upgrade`コマンドを実行して、`my-nginx`のレプリカ数を2に更新して下さい。

## Answer

```bash
> helm repo add bitnami https://charts.bitnami.com/bitnami
"bitnami" has been added to your repositories

> helm search repo bitnami/nginx
NAME                                    CHART VERSION   APP VERSION     DESCRIPTION                                       
bitnami/nginx                           22.3.3          1.29.3          NGINX Open Source is a web server that can be a...
bitnami/nginx-ingress-controller        12.0.7          1.13.1          NGINX Ingress Controller is an Ingress controll...
bitnami/nginx-intel                     2.1.15          0.4.9           DEPRECATED NGINX Open Source for Intel is a lig...

> k create ns ckad-helm
namespace/ckad-helm created

> helm install my-nginx bitnami/nginx -n ckad-helm
NAME: my-nginx
LAST DEPLOYED: Sat Nov 29 02:24:13 2025
NAMESPACE: ckad-helm
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: nginx
CHART VERSION: 22.3.3
APP VERSION: 1.29.3

⚠ WARNING: Since August 28th, 2025, only a limited subset of images/charts are available for free.
    Subscribe to Bitnami Secure Images to receive continued support and security updates.
    More info at https://bitnami.com and https://github.com/bitnami/containers/issues/83267

** Please be patient while the chart is being deployed **
NGINX can be accessed through the following DNS name from within your cluster:

    my-nginx.ckad-helm.svc.cluster.local (port 80)

To access NGINX from outside the cluster, follow the steps below:

1. Get the NGINX URL by running these commands:

  NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        Watch the status with: 'kubectl get svc --namespace ckad-helm -w my-nginx'

    export SERVICE_PORT=$(kubectl get --namespace ckad-helm -o jsonpath="{.spec.ports[0].port}" services my-nginx)
    export SERVICE_IP=$(kubectl get svc --namespace ckad-helm my-nginx -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
    echo "http://${SERVICE_IP}:${SERVICE_PORT}"
WARNING: Rolling tag detected (bitnami/nginx:latest), please note that it is strongly recommended to avoid using rolling tags in a production environment.
+info https://techdocs.broadcom.com/us/en/vmware-tanzu/application-catalog/tanzu-application-catalog/services/tac-doc/apps-tutorials-understand-rolling-tags-containers-index.html
WARNING: Rolling tag detected (bitnami/git:latest), please note that it is strongly recommended to avoid using rolling tags in a production environment.
+info https://techdocs.broadcom.com/us/en/vmware-tanzu/application-catalog/tanzu-application-catalog/services/tac-doc/apps-tutorials-understand-rolling-tags-containers-index.html
WARNING: Rolling tag detected (bitnami/nginx-exporter:latest), please note that it is strongly recommended to avoid using rolling tags in a production environment.
+info https://techdocs.broadcom.com/us/en/vmware-tanzu/application-catalog/tanzu-application-catalog/services/tac-doc/apps-tutorials-understand-rolling-tags-containers-index.html

WARNING: There are "resources" sections in the chart not set. Using "resourcesPreset" is not recommended for production. For production installations, please set the following values according to your workload needs:
  - cloneStaticSiteFromGit.gitSync.resources
  - resources
+info https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/

> helm list -n ckad-helm
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
my-nginx        ckad-helm       1               2025-11-29 02:24:13.191054522 +0000 UTC deployed        nginx-22.3.3    1.29.3     

> k get deploy -n ckad-helm 
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
my-nginx   1/1     1            1           54s

> helm upgrade my-nginx bitnami/nginx -n ckad-helm --set replicaCount=2

> kubectl get deploy -n ckad-helm 
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
my-nginx   2/2     2            2           111s
```