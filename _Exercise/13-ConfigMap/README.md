# 13-ConfigMap

## Question

`web`名前空間で実行されている`my-web` Deploymentは、nginxイメージコンテナを実行するPodを管理しています。
DeploymentはNodePortタイプのサービスで公開されており、`curl controlplane:32100`を実行してコンテナに接続できます。
コンテナが表示する`index.html`ファイルを、`updated_index.html`に変更する必要があります。

`index.html`をキー、`updated_index.html`ファイルをバリューとして保持する`ConfigMap`を作成し、
`/usr/share/nginx/html`ディレクトリにマウントされているConfigMapを更新して下さい。`ConfigMap`の名前は`new-index-cm`とします。

## Answer

```bash
> k create cm -n web new-index-cm --from-file=index.html=updated_index.html
configmap/new-index-cm created

> curl controlplane:32100
old

> k edit -n web deployment my-web 
deployment.apps/my-web edited

> curl controlplane:32100
new
```