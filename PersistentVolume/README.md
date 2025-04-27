# PersistentVolume

```bash
vi my-pv.yaml

k apply -f my-pv.yaml 
persistentvolume/my-pv created

vi my-claim.yaml

k apply -f my-claim.yaml 
persistentvolumeclaim/my-claim created

k run pv-pod --image=nginx $do > pv-pod.yaml

vi pv-pod.yaml

k apply -f pv-pod.yaml
pod/pv-pod created

k get pv,pvc,pods
NAME                     CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM              STORAGECLASS   VOLUMEATTRIBUTESCLASS   REASON   AGE
persistentvolume/my-pv   1Gi        RWX            Retain           Bound    default/my-claim   sc             <unset>                          15m

NAME                             STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
persistentvolumeclaim/my-claim   Bound    my-pv    1Gi        RWX            sc             <unset>                 19s

NAME         READY   STATUS    RESTARTS   AGE
pod/pv-pod   1/1     Running   0          2m11s
```
