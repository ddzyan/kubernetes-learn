## 简介

创建多个任务去执行 pi 的取值运算，当运算完毕后，进程将退出。

## 操作

```sh
$ kubectl create -f ./pod.yaml

$ kubectl describe job/pi
Name:           pi
Namespace:      default
Selector:       controller-uid=c196d4aa-e44b-42bd-ad5e-6e8da7acc3b6
Labels:         controller-uid=c196d4aa-e44b-42bd-ad5e-6e8da7acc3b6
                job-name=pi
Annotations:    revisions:
                  {"1":{"status":"running","desire":1,"uid":"c196d4aa-e44b-42bd-ad5e-6e8da7acc3b6","start-time":"2020-09-20T22:49:55+08:00","completion-time...
Parallelism:    1
Completions:    1
Start Time:     Sun, 20 Sep 2020 22:49:55 +0800
Pods Statuses:  1 Running / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  controller-uid=c196d4aa-e44b-42bd-ad5e-6e8da7acc3b6
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
  Type    Reason            Age    From            Message
  ----    ------            ----   ----            -------
  Normal  SuccessfulCreate  2m28s  job-controller  Created pod: pi-pmmsg

```

```sh
# DESIRED 最小完成数量，SUCCESSFUL已经完成的数量
$ kubectl get job
NAME      DESIRED   SUCCESSFUL   AGE
pi        4         0            3s
```
