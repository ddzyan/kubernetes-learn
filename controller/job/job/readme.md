## 简介

创建批量任务去执行 pi 的取值运算，当运算完毕后，进程将退出。任务完成后，pod 会一直存在不会自动删除，如果要对 job 进行管理可以使用以下方法：

- CronJob
- ttlSecondsAfterFinished

## 操作

```sh
$ kubectl create -f ./pod.yaml

$ kubectl describe job/pi
Name:           pi
Namespace:      default
Selector:       controller-uid=47f29ffe-c627-4eb5-bde5-2805b1a2c297
Labels:         controller-uid=47f29ffe-c627-4eb5-bde5-2805b1a2c297
                job-name=pi
Annotations:    revisions:
                  {"1":{"status":"running","desire":4,"uid":"47f29ffe-c627-4eb5-bde5-2805b1a2c297","start-time":"2020-09-21T10:01:48+08:00","completion-time...
Parallelism:    2
Completions:    4
Start Time:     Mon, 21 Sep 2020 10:01:48 +0800
Pods Statuses:  2 Running / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  controller-uid=47f29ffe-c627-4eb5-bde5-2805b1a2c297
           job-name=pi
  Containers:
   pi:
    Image:      resouer/ubuntu-bc
    Port:       <none>
    Host Port:  <none>
    Command:
      sh
      -c
      echo 'scale=10000;4*a(1)' | bc -l
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age   From            Message
  ----    ------            ----  ----            -------
  Normal  SuccessfulCreate  47s   job-controller  Created pod: pi-5jgj2
  Normal  SuccessfulCreate  47s   job-controller  Created pod: pi-2l4gl

```

```sh
# 查看 job 创建的 pod 信息
$ kubectl get po
NAME                    READY   STATUS    RESTARTS   AGE
pi-2l4gl                1/1     Running   0          112s
pi-5jgj2                1/1     Running   0          112s

# 查看 job 完成情况
$ kubectl logs pi-2l4gl

# COMPLETIONS 完成进度
$ kubectl get job/pi
NAME   COMPLETIONS   DURATION   AGE
pi     4/4           3m48s      6m22s

# 删除 job 创建的所有 pod
$ kubectl delete job --all
```
