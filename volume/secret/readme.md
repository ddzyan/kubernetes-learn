## 简介

k8s secret 操作示例

### 案例一 demo1

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

### 案例二 demo2

#### 创建配置

现在需要创建一个 secret 保存：用户名：root，密码：datahome123 信息

首先对需要保存对信息进行 base64 转码

```shell
$ echo "root" | base64
cm9vdAo=

$ echo "datahome123" | base64
ZGF0YWhvbWUxMjMK
```

编写 secret.yaml 文件

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  user: cm9vdAo=
  pass: ZGF0YWhvbWUxMjMK
```

#### 创建

```shell
# 创建 secret
$ kubectl create -f secret.yaml

$ kubectl describe secret my-secret
Name:         my-secret
Namespace:    default
Labels:       <none>
Annotations:  <none>

Type:  Opaque

Data
====
pass:  12 bytes
user:  5 bytes

# 创建 pod
$ kubectl create -f ./pod.yaml
```

```shell
# 验证是否挂载
$ kubectl exec  my-pod -- ls /mypod-vol
pass
user

$ kubectl exec  my-pod -- cat /mypod-vol/user
root
```
