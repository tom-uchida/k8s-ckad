# 1-PersistentVolume

## Question

Create a Persistent Volume called log-volume.
It should make use of a storage class name manual.
It should use RWX as the access mode and have a size of 1Gi.
The volume should use the hostPath /opt/volume/nginx

Next, create a PVC called log-claim requesting a minimum of 200Mi of storage.
This PVC should bind to log-volume.

Mount this in a pod called logger at the location /var/www/nginx.
This pod should use the image nginx:alpine.

## Answer

```bash
vi log-volume.yaml

k apply -f log-volume.yaml 
persistentvolume/log-volume created

vi log-claim.yaml

k apply -f log-claim.yaml 
persistentvolumeclaim/log-claim created

k run logger --image=nginx:alpine --dry-run=client -o yaml > logger.yaml

k apply -f logger.yaml 
pod/logger created
```
