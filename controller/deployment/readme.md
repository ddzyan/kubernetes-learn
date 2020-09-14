## 简介

使用 deployment 控制器来管理 pod ，如果 pod 数量超过 deployment 设定的 replicas 则会删除多余的 pod，反之如果 pod 数量超出则会创建新的 pod。

### 使用

```shell
# 创建 deployment
$ kubectl apply -f deploy.yaml
deployment.apps/deploy-myapp created

$ kubectl get pod


# 使用命令式修改 replicas 进行 pod 扩展
$ kubectl scale --replicas=2 deploy/deploy-myapp

$ kubectl get po
deploy-myapp-7b5f8dfc4d-2fqgc   1/1     Running   0          18m
deploy-myapp-7b5f8dfc4d-dzd24   1/1     Running   0          26s
```
