# logging

```bash
k create ns logging
namespace/logging created

k run logger --image=busybox -n logging --command -- sh -c "while true; do echo 'Hello'; sleep 4; done"
pod/logger created

k logs -n logging logger --since=20s --timestamps > /etc/hello.log

cat /etc/hello.log 
2025-04-29T13:19:23.547038448Z Hello
2025-04-29T13:19:27.548428183Z Hello
2025-04-29T13:19:31.549703862Z Hello
2025-04-29T13:19:35.551035637Z Hello
2025-04-29T13:19:39.552521479Z Hello

k get pods -n logging
NAME     READY   STATUS    RESTARTS   AGE
logger   1/1     Running   0          116s
```