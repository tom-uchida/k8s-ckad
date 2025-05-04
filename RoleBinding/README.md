# RoleBinding

```bash
k create sa deployer-sa
serviceaccount/deployer-sa created

k create role deployer-role --verb=create --resource=deployments
role.rbac.authorization.k8s.io/deployer-role created

k create rolebinding deployer-binding --serviceaccount=default:deployer-sa --role=deployer-role
rolebinding.rbac.authorization.k8s.io/deployer-binding created

k auth can-i create deployments --as=system:serviceaccount:default:deployer-sa
yes
```
