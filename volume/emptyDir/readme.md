## 简介

在宿主机上创建一个 emptyDir 卷 特点是：

- 目录初始为空
- pod 在节点上运行，则 卷 就会一直存在
- pod 从节点上删除，则 卷 也会永久删除

主要用途：

- 临时目录
- 为耗时较长的计算任务提供检查点，以便任务能方便地从崩溃前状态恢复执行。
- 在 Web 服务器容器服务数据时，保存内容管理器容器获取的文件。

### 操作

```
$ kubectl create -f ./pod.yaml

$ kubectl get po -o wide
NAME    READY   STATUS    RESTARTS   AGE   IP            NODE    NOMINATED NODE   READINESS GATES
myapp   1/1     Running   0          11m   10.244.1.13   node2   <none>           <none>

$ kubectl get svc
NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
myapp        ClusterIP   10.103.23.104   <none>        3000/TCP   11m

$ curl 10.103.23.104:3000
```

此时可以进入 node2 节点的 `/var/lib/kubelet/pods/861c6edf-f698-4191-97c9-7615bd552b8e/volumes/kubernetes.io~empty-dir/cache-volume` 已经生成日志文件，删除 pod 则文件夹也会被删除
