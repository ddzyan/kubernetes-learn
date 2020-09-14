## 简介

k8s secret 操作示例

### 案例一

通过命令式直接创建 secret 对象，具体操作说明可以参考如下指令

```shell
$ kubectl create secret --help
```

#### 创建配置文件

```shell
$ kubectl create secret generic user --from-file=./file/username.txt
$ kubectl create secret generic pass --from-file=./file/password.txt

$ kubectl get secret
NAME                  TYPE                                  DATA   AGE
pass                  Opaque                                1      20m
user                  Opaque                                1      21m

# 查看信息
$ kubectl describe secret user
Name:         user
Namespace:    default
Labels:       <none>
Annotations:  <none>

Type:  Opaque

Data
====
username.txt:  6 bytes
```

#### 创建 pod 并且使用上面的 secret

```shell
$ kubectl create -f ./file_config_pod.yaml

# 查看运行状态
$ kubectl get po
NAME                    READY   STATUS    RESTARTS   AGE
test-projected-volume   1/1     Running   0          14m

# 进入容器查看挂载文件
$ kubectl exec test-projected-volume -- cat /projected-volume/username.txt
admin
$ kubectl exec test-projected-volume -- cat /projected-volume/password.txt
admin
```
