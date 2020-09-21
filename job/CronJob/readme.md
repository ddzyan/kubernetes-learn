## 简介

CronJob 可以基于特点的清理策略将 job 清理掉，CronJob 仅负责创建与其调度时间相匹配的 Job，而 Job 又负责管理其代表的 Pod。

## 操作

创建一个 1 分钟执行一次的 job，完成的 job 会被自动删除

```sh
# 创建
$ kubectl create -f ./pod.yaml

# 查看信息
$ kubectl describe -f ./pod.yaml
Name:                          hello
Namespace:                     default
Labels:                        <none>
Annotations:                   <none>
Schedule:                      */1 * * * *
Concurrency Policy:            Allow
Suspend:                       False
Successful Job History Limit:  3 # 任务完成情况
Failed Job History Limit:      1 # 任务失败情况
Starting Deadline Seconds:     <unset>
Selector:                      <unset>
Parallelism:                   <unset>
Completions:                   <unset>
Pod Template:
  Labels:  <none>
  Containers:
   hello:
    Image:      busybox
    Port:       <none>
    Host Port:  <none>
    Args:
      /bin/sh
      -c
      date; echo Hello from the Kubernetes cluster
    Environment:     <none>
    Mounts:          <none>
  Volumes:           <none>
Last Schedule Time:  Mon, 21 Sep 2020 10:31:00 +0800
Active Jobs:         <none>
Events:
  Type    Reason            Age    From                Message
  ----    ------            ----   ----                -------
  Normal  SuccessfulCreate  3m27s  cronjob-controller  Created job hello-1600655280
  Normal  SawCompletedJob   3m17s  cronjob-controller  Saw completed job: hello-1600655280, status: Complete
  Normal  SuccessfulCreate  2m27s  cronjob-controller  Created job hello-1600655340
  Normal  SawCompletedJob   2m17s  cronjob-controller  Saw completed job: hello-1600655340, status: Complete
  Normal  SuccessfulCreate  87s    cronjob-controller  Created job hello-1600655400
  Normal  SawCompletedJob   77s    cronjob-controller  Saw completed job: hello-1600655400, status: Complete
  Normal  SuccessfulCreate  27s    cronjob-controller  Created job hello-1600655460
  Normal  SawCompletedJob   17s    cronjob-controller  Saw completed job: hello-1600655460, status: Complete
  Normal  SuccessfulDelete  17s    cronjob-controller  Deleted job hello-1600655280
```
