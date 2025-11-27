# 23-Service

## Question

`server`名前空間で作成されている`webapp` Podは、nodeコンテナ上で`Express.js`を実行しています。
Podは同じ名前空間に作成されている`websvc` Serviceによって公開される必要があります。

現在、`websvc` Serviceを通じてwebapp Podに接続することができません。
`websvc` Serviceの構成を確認し、問題の原因を修正してください。
なお、変更は`websvc`にのみ適用し、`webapp` Podは変更しないで下さい。

## Answer