# security-context

```bash
k run context --image=busybox $do --command -- sh -c "sleep 3000" > context.yaml

vi context.yaml 

k apply -f context.yaml 
pod/context created

k exec -it context -- id
uid=1000 gid=3000 groups=3000
```
