# scale

```bash
k create deploy frontend --image=nginx --replicas=2
deployment.apps/frontend created

k get deploy
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
frontend   2/2     2            2           35s

k scale deploy frontend --replicas=5
deployment.apps/frontend scaled

k get deploy
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
frontend   5/5     5            5           64s
```
