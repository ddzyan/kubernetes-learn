## 简介

volume 各种存储的使用 demo

### 备注

1. hostPath 和 emptyDir 都是将提供一个宿主机目录为存储卷，有什么区别？

- hostPath 如果 Pod 被删除，数据卷还是会保存在宿主机上
- emptyDir 只有 pod 存在才不会被删除，如果被删除则数据卷也会被删除
