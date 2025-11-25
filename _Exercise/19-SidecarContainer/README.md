# 19-SidecarContainer

## Question

`adapter`名前空間において、`logger`という名前のPodが`busybox`イメージを使用してコンテナを実行しています。
このコンテナは、10秒ごとに`date`コマンドの結果をJSON形式で`input.log`ファイルに記録します。Podは`emptyDir`ボリュームを`/tmp/log`ディレクトリにマウントし、`input.log`ファイルをそこに保存します。

Podに`fluent/fluentd:edge`イメージを使用したコンテナを追加し、`/tmp/log/input.log`の内容を`/tmp/log/output/`ディレクトリ内の`buffer`ファイルに出力します。次の手順を実行して下さい。

1. コンテナ名を`fluentd`に設定して下さい
2. `logger`コンテナと共有するボリュームを`/tmp/log`ディレクトリにマウントして下さい。
3. `/fluentd/etc`ディレクトリに`fluentd-config`をマウントして下さい。

## Answer

```bash
> k exec -it -n adapter logger -- cat /tmp/log/input.log
{"dt": "Tue Nov 25 10:30:33 UTC 2025"}
{"dt": "Tue Nov 25 10:30:43 UTC 2025"}
{"dt": "Tue Nov 25 10:30:53 UTC 2025"}

> vi logger.yaml 

> k replace -f logger.yaml --force
pod "logger" deleted from adapter namespace
pod/logger replaced

> k get -n adapter pod
NAME     READY   STATUS    RESTARTS   AGE
logger   2/2     Running   0          23s

> k exec -it -n adapter logger -c logger -- sh                
/ # ls /tmp/log/output/
buffer.b64468fa3393b3d4a3223dfcacdf6d18f.log       buffer.b64468fa3393b3d4a3223dfcacdf6d18f.log.meta
/ # tail /tmp/log/output/buffer.b64468fa3393b3d4a3223dfcacdf6d18f.log
2025-11-25T10:46:05+00:00       logger.format1  {"dt":"Tue Nov 25 10:46:04 UTC 2025"}
2025-11-25T10:46:15+00:00       logger.format1  {"dt":"Tue Nov 25 10:46:14 UTC 2025"}
2025-11-25T10:46:25+00:00       logger.format1  {"dt":"Tue Nov 25 10:46:24 UTC 2025"}
2025-11-25T10:46:35+00:00       logger.format1  {"dt":"Tue Nov 25 10:46:34 UTC 2025"}
2025-11-25T10:46:45+00:00       logger.format1  {"dt":"Tue Nov 25 10:46:44 UTC 2025"}
2025-11-25T10:46:55+00:00       logger.format1  {"dt":"Tue Nov 25 10:46:54 UTC 2025"}
2025-11-25T10:47:05+00:00       logger.format1  {"dt":"Tue Nov 25 10:47:04 UTC 2025"}
2025-11-25T10:47:15+00:00       logger.format1  {"dt":"Tue Nov 25 10:47:14 UTC 2025"}
2025-11-25T10:47:25+00:00       logger.format1  {"dt":"Tue Nov 25 10:47:24 UTC 2025"}
2025-11-25T10:47:35+00:00       logger.format1  {"dt":"Tue Nov 25 10:47:34 UTC 2025"}
```