## 简介

使用 statefulSet 创建有状态到服务，它的特点是使用 Pod 模板创建 Pod 的时候，会对 Pod 进行编号，并且按照编号顺序逐一完成创建工作。

### headerLess

使用 service 类型 ClusterIP 并且将 IP 设定为 none 创建无头服务，使必须使用 DNS 或者 hostname 的方式访问这些 Pod 的 IP 地址。

Headless Service 之后，它所代理的所有 Pod 的 IP 地址，都会被绑定一个这样格式的 DNS 记录，如下所示

```
<pod-name>.<svc-name>.<namespace>.svc.cluster.local
```

#### 部署

```shell
$ kubectl create -f svc.yaml

$ kubectl create -f sts.yaml

#查看 pod 状态
$ kubectl get po -w -l app=nginx
NAME    READY   STATUS    RESTARTS   AGE
web-0   1/1     Running   0          3m
web-1   1/1     Running   0          2m58s
```

pod 的名称会按照 statefulSetName + 创建顺序 ，并且在上一个未达到 Running 状态，下一个 pod 不会创建。

通过 statefulSet 创建的 Pod 的名称与 container 内的 hostname 一致。

```shell
$ kubectl exec web-0 -- sh -c 'hostname'
web-0

$ kubectl exec web-1 -- sh -c 'hostname'
web-1

# 创建一个新的容器查看 dns 映射的 ip 地址,发现地址成功解析为对应 pod 的 ip 地址
$ kubectl run -i --tty --image busybox:1.28.4 dns-test --restart=Never --rm /bin/sh
$ nslookup web-0.svc-nginx
Server:    10.96.0.10
Address 1: 10.96.0.10 kube-dns.kube-system.svc.cluster.local

Name:      web-0.svc-nginx
Address 1: 10.244.1.79 web-0.svc-nginx.default.svc.cluster.local
```
