# set-image

```bash
k create deploy nginx-app --image=nginx:stable --replicas=3
deployment.apps/nginx-app created

k get deploy -o wide
NAME        READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES         SELECTOR
nginx-app   3/3     3            3           31s     nginx        nginx:stable   app=nginx-app

k set image deploy nginx-app nginx=nginx:mainline
deployment.apps/nginx-app image updated

k get deploy -o wide
NAME        READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES         SELECTOR
nginx-app   3/3     3            3           73s     nginx        nginx:mainline   app=nginx-app
```
