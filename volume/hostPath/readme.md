## 简介

使用 hostPath 存储卷，将 pod 的文件或者文件夹挂载在宿主机指定目录上，此存储不会因为 pod 删除而删除，支持以下主要类型：

- Directory 指定路径必须有目录，不存在则 pod 会启动失败
- FileOrCreate 不存在则创建，创建的权限和 kubelet 一致
- File 指定路径必须有文件

### 操作

```sh
$ kubectl create -f pod.yaml

$ kubectl get svc
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
myapp        ClusterIP   10.109.145.142   <none>        3000/TCP   2m51s

$ curl 10.109.145.142:3000
{"version":"1.0.7","url":"/","nodeName":"node2","myPodName":"myapp","myPodNamespace":"default","myPodIp":"10.244.1.11"}

$ kubectl get po -o wide
NAME    READY   STATUS    RESTARTS   AGE     IP            NODE    NOMINATED NODE   READINESS GATES
myapp   1/1     Running   0          4m10s   10.244.1.11   node2   <none>           <none>

```

远程连接到宿主机目录，查看 /root/bill/vols/log 下已经产生日志
