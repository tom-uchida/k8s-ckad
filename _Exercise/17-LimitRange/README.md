# 17-LimitRange

## Question

`resource-management`名前空間では、`cpu-resource-constraint`というLimitRangeによって、
CPUリソース使用量の最大値が定義されています。

`nginx`イメージを使用して`managed`というPodを作成して下さい。
なお、Podには以下の条件を満たすリソース管理を設定して下さい。

- コンテナのCPUリソース要求として、`200m`を設定して下さい。
- `resource-management1名前空間に設定された最大cpu制約の半分を、コンテナのリソース制限として設定して下さい。

## Answer

```bash
> k describe -n resource-management limitranges cpu-resource-constraint       
Name:       cpu-resource-constraint
Namespace:  resource-management
Type        Resource  Min  Max   Default Request  Default Limit  Max Limit/Request Ratio
----        --------  ---  ---   ---------------  -------------  -----------------------
Container   cpu       -    900m  900m             900m           -

> k -n resource-management run managed --image=nginx --dry-run=client -oyaml > managed.yaml

> vi managed.yaml

> k apply -f managed.yaml 
pod/managed created
```