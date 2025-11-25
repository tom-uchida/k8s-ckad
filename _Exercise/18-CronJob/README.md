# 18-CronJob

## Question

1. `cron`という名前空間を作成し、以下の条件を満たすCronJobを作成して下さい。
   - コンテナイメージは`alpine`を使用し、CronJobの名前は`ps-cron`とします。
   - `ps-cron`は"ps aux"コマンドを1分毎に実行し、成功したJobを5、失敗したJobを3まで保存します。
   - また、Jobは開始から6秒経過したPodを終了させます。
2. CronJobからJobを作成して下さい。Job名は`ps-job`とします。

## Answer

```bash
> k create ns cron
namespace/cron created

> k create cronjob -n cron ps-cron --image=alpine --schedule="*/1 * * * *" --dry-run=client -oyaml > ps-cron.ya
ml

> vi ps-cron.yaml

> k apply -f ps-cron.yaml
cronjob.batch/ps-cron created

> k create job -n cron ps-job --from=cronjob/ps-cron
job.batch/ps-job created

> k get -n cron cj,job
NAME                    SCHEDULE      TIMEZONE   SUSPEND   ACTIVE   LAST SCHEDULE   AGE
cronjob.batch/ps-cron   */1 * * * *   <none>     False     0        24s             6m24s

NAME                         STATUS     COMPLETIONS   DURATION   AGE
job.batch/ps-cron-29401098   Complete   1/1           4s         84s
job.batch/ps-cron-29401099   Complete   1/1           4s         24s
job.batch/ps-job             Complete   1/1           4s         98s
```