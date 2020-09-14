## 简介
k8s secret 操作示例

### 案例一
通过命令式直接创建 serect 对象，具体操作说明可以参考如下指令

```shell
$ kubectl create secret --help
```

###  创建配置文件
```shell
$ kubectl create secret generic user --from-file=./file/username.txt
$ kubectl create secret generic pass --from-file=./file/password.txt
```

### 创建 pod

```shell
$ kubectl create -f ./file_config_pod.yaml
```
