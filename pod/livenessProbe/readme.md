## 简介

在 pod 中使用 liveness 探针做 container 的健康检测，支持的方式如下：

- exec
- http
- tcp

### 部署

```shell
$ kubectl create -f ./pod.yaml
```
