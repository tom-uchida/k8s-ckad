# 6-LivenessProve

## Question

We have deployed a few pods in this cluster in various namespaces.
Inspect them and identify the pod which is not in a Ready state.
Troubleshoot and fix the issue.

Next, add a check to restart the container on the same pod if the command ls /var/www/html/file_check fails.
This check should start after a delay of 10 seconds and run every 60 seconds.

You may delete and recreate the object. Ignore the warnings from the probe.

## Answer

```bash
k get pod --all-namespaces 
NAMESPACE     NAME                                       READY   STATUS    RESTARTS   AGE
default       dev-pod-dind-878516                        3/3     Running   0          106s
default       pod-xyz1123                                1/1     Running   0          106s
default       webapp-color                               1/1     Running   0          105s
dev0403       nginx0403                                  1/1     Running   0          106s
dev0403       pod-dar85                                  1/1     Running   0          106s
dev1401       nginx1401                                  0/1     Running   0          106s
dev1401       pod-kab87                                  1/1     Running   0          106s
dev2406       nginx2406                                  1/1     Running   0          106s
dev2406       pod-var2016                                1/1     Running   0          106s
e-commerce    e-com-1123                                 1/1     Running   0          105s
kube-system   calico-kube-controllers-5745477d4d-dljfm   1/1     Running   0          16m
kube-system   canal-fcm8b                                2/2     Running   0          16m
kube-system   canal-w55cc                                2/2     Running   0          16m
kube-system   coredns-7484cd47db-84mcs                   1/1     Running   0          16m
kube-system   coredns-7484cd47db-w7xsb                   1/1     Running   0          16m
kube-system   etcd-controlplane                          1/1     Running   0          16m
kube-system   kube-apiserver-controlplane                1/1     Running   0          16m
kube-system   kube-controller-manager-controlplane       1/1     Running   0          16m
kube-system   kube-proxy-4lpbr                           1/1     Running   0          16m
kube-system   kube-proxy-rq6m4                           1/1     Running   0          16m
kube-system   kube-scheduler-controlplane                1/1     Running   0          16m
marketing     redis-556f566f7f-8csgx                     1/1     Running   0          105s

k get pod nginx1401 -n dev1401 -o yaml > nginx1401.yaml

vi nginx1401.yaml

k replace -f nginx1401.yaml --force
pod "nginx1401" deleted
pod/nginx1401 replaced

k get pod --all-namespaces 
NAMESPACE     NAME                                       READY   STATUS    RESTARTS   AGE
default       dev-pod-dind-878516                        3/3     Running   0          9m9s
default       pod-xyz1123                                1/1     Running   0          9m9s
default       webapp-color                               1/1     Running   0          9m8s
dev0403       nginx0403                                  1/1     Running   0          9m9s
dev0403       pod-dar85                                  1/1     Running   0          9m9s
dev1401       nginx1401                                  1/1     Running   0          11s
dev1401       pod-kab87                                  1/1     Running   0          9m9s
dev2406       nginx2406                                  1/1     Running   0          9m9s
dev2406       pod-var2016                                1/1     Running   0          9m9s
e-commerce    e-com-1123                                 1/1     Running   0          9m8s
kube-system   calico-kube-controllers-5745477d4d-dljfm   1/1     Running   0          24m
kube-system   canal-fcm8b                                2/2     Running   0          23m
kube-system   canal-w55cc                                2/2     Running   0          24m
kube-system   coredns-7484cd47db-84mcs                   1/1     Running   0          24m
kube-system   coredns-7484cd47db-w7xsb                   1/1     Running   0          24m
kube-system   etcd-controlplane                          1/1     Running   0          24m
kube-system   kube-apiserver-controlplane                1/1     Running   0          24m
kube-system   kube-controller-manager-controlplane       1/1     Running   0          24m
kube-system   kube-proxy-4lpbr                           1/1     Running   0          23m
kube-system   kube-proxy-rq6m4                           1/1     Running   0          24m
kube-system   kube-scheduler-controlplane                1/1     Running   0          24m
marketing     redis-556f566f7f-8csgx                     1/1     Running   0          9m8s
```
