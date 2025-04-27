# CronJob

```bash
k create cj cron-pi --image=perl --schedule="*/1 * * * *" $do > cron-pi.yaml

vi cron-pi.yaml 

k apply -f cron-pi.yaml 
cronjob.batch/cron-pi created

k get cj
NAME      SCHEDULE      TIMEZONE   SUSPEND   ACTIVE   LAST SCHEDULE   AGE
cron-pi   */1 * * * *   <none>     False     0        17s             2m8s

watch -n 5 kubectl get cj,pods
Every 5.0s: kubectl get cj,pods                                                                                               controlplane: Sun Apr 27 09:56:24 2025

NAME                    SCHEDULE      TIMEZONE   SUSPEND   ACTIVE   LAST SCHEDULE   AGE
cronjob.batch/cron-pi   */1 * * * *   <none>     False     0        24s             5m15s

NAME                         READY   STATUS      RESTARTS   AGE
pod/cron-pi-29095794-6kj9b   0/1     Completed   0          2m20s
pod/cron-pi-29095794-h4759   0/1     Completed   0          2m24s
pod/cron-pi-29095794-kr5jl   0/1     Completed   0          2m16s
pod/cron-pi-29095794-n4g6k   0/1     Completed   0          2m20s
pod/cron-pi-29095794-wpcnk   0/1     Completed   0          2m24s
pod/cron-pi-29095795-668mq   0/1     Completed   0          80s
pod/cron-pi-29095795-72xbk   0/1     Completed   0          84s
pod/cron-pi-29095795-7zqk5   0/1     Completed   0          81s
pod/cron-pi-29095795-mmnkg   0/1     Completed   0          77s
pod/cron-pi-29095795-vrzg9   0/1     Completed   0          84s
pod/cron-pi-29095796-22vn5   0/1     Completed   0          21s
pod/cron-pi-29095796-r5q7v   0/1     Completed   0          17s
pod/cron-pi-29095796-rjjvd   0/1     Completed   0          24s
pod/cron-pi-29095796-td54v   0/1     Completed   0          24s
pod/cron-pi-29095796-tsflx   0/1     Completed   0          20s
```
