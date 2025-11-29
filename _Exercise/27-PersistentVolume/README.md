# 27-PersistentVolume

## Question

`persistent`名前空間では、`ckad-pv` Persistent Volumeと
`ckad-pv-claim` Persistent Volume Claimが作成されています。
`ckad-pv` は、`ckad-pv-claim` をバインドする必要があります。

`ckad-pv-claim`のSTATUSが`Pending`になっている原因を特定し、`Bound`になるように修正して下さい。
なお、修正にはダウンロードした`ckad-pv-claim.yaml`ファイルを使用し、`ckad-pv` は変更しないで下さい。

## Answer

```bash
> k get -n persistent pv,pvc
NAME                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   VOLUMEATTRIBUTESCLASS   REASON   AGE
persistentvolume/ckad-pv   500Mi      RWO            Retain           Available           standard       <unset>                          11s

NAME                                  STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
persistentvolumeclaim/ckad-pv-claim   Pending                                      special        <unset>                 11s

> vi ckad-pv-claim.yaml 

> k replace -f ckad-pv-claim.yaml --force
persistentvolumeclaim "ckad-pv-claim" deleted from persistent namespace

> k get -n persistent pv,pvc
NAME                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                      STORAGECLASS   VOLUMEATTRIBUTESCLASS   REASON   AGE
persistentvolume/ckad-pv   500Mi      RWO            Retain           Bound    persistent/ckad-pv-claim   standard       <unset>                          3m51s

NAME                                  STATUS   VOLUME    CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
persistentvolumeclaim/ckad-pv-claim   Bound    ckad-pv   500Mi      RWO            standard       <unset>                 18s
```