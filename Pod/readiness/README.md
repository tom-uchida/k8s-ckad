# readiness

```bash
k run exec-readiness --image=busybox $do --command -- sh -c "mkdir -p /etc/ready/probe; sleep 3600;" > exec-readiness.yaml 

vi exec-readiness.yaml 

k apply -f exec-readiness.yaml 
pod/exec-readiness created

k get pods
NAME             READY   STATUS             RESTARTS        AGE
exec-readiness   1/1     Running            0               28s
```
