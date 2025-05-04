# resource

```bash
k run resource --image=nginx $do > resource.yaml

vi resource.yaml 

k apply -f resource.yaml 
pod/resource created

k describe pod resource | grep -e Limits -e cpu -e memory -e Requests
    Limits:
      cpu:     1
      memory:  2Gi
    Requests:
      cpu:        500m
      memory:     1Gi
```
