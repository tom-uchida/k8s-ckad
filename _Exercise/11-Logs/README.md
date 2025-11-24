# 11-Logs

## Question

`filter`名前空間では、pod-1からpod-10までの10個のPodが実行されています。
それぞれのPodには、`app: "Pod名"`のラベルが付与されています。
以下のラベルを持つPodのログを、/etc/pods.logに出力して下さい。

- `app: pod-3`
- `app: pod-7`
- `app: pod-8`

## Answer

```bash
> k logs -l 'app in (pod-3,pod-7,pod-8)' -n filter > /etc/pods.log

> cat /etc/pods.log 
Hello from pod-3
Hello from pod-7
Hello from pod-8
```