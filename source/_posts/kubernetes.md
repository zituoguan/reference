---
title: Kubernetes
date: 2023-01-09 10:26:55
background: bg-[#416cde]
tags:
  - config
  - format
categories:
  - 编程
intro: |
  此页面包含常用 kubectl 命令和标志的列表。
plugins:
  - copyCode
---

## 查看和查找资源 {.cols-2}

### 节点

```bash
kubectl get no # 显示所有节点信息
kubectl get no -o wide # 显示所有节点的更多信息
kubectl describe no # 显示节点详细信息
kubectl get no -o yaml # 以 yaml 格式显示节点详细信息
kubectl get node --selector=[label_name] # 筛选具有指定标签的节点
kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type="ExternalIP")].address}'
# 输出由 jsonpath 表达式定义的字段信息
kubectl top node [node_name] # 显示节点（CPU/内存/存储）使用情况
```

资源名称：nodes，缩写：no

### Pods

```bash
kubectl get po # 显示所有容器组信息
kubectl get po -o wide
kubectl describe po
kubectl get po --show-labels # 查看容器组的标签
kubectl get po -l app=nginx
kubectl get po -o yaml
kubectl get pod [pod_name] -o yaml --export
kubectl get pod [pod_name] -o yaml --export > nameoffile.yaml
# 将容器组信息以 yaml 格式导出到 yaml 文件
kubectl get pods --field-selector status.phase=Running
# 使用字段选择器筛选出容器组信息
```

资源名称：pods，缩写：po

### 命名空间

```bash
kubectl get ns
kubectl get ns -o yaml
kubectl describe ns
```

资源名称：namespaces，缩写：ns

### Deployments

```bash
kubectl get deploy
kubectl describe deploy
kubectl get deploy -o wide
kubectl get deploy -o yaml
```

资源名称：deployments，缩写：deploy

### Services

```bash
kubectl get svc
kubectl describe svc
kubectl get svc -o wide
kubectl get svc -o yaml
kubectl get svc --show-labels
```

资源名称：services，缩写：svc

### Daemon Sets

```bash
kubectl get ds
kubectl describe ds --all-namespaces
kubectl describe ds [daemonset_name] -n [namespace_name]
kubectl get ds [ds_name] -n [ns_name] -o yaml
```

资源名称：daemonsets，缩写：ds

### Events

```bash
kubectl get events
kubectl get events -n kube-system
kubectl get events -w
```

资源名称：events，缩写：ev

### 日志

```bash
kubectl logs [pod_name]
kubectl logs --since=1h [pod_name]
kubectl logs --tail=20 [pod_name]
kubectl logs -f -c [container_name] [pod_name]
kubectl logs [pod_name] > pod.log
```

### 服务账户

```bash
kubectl get sa
kubectl get sa -o yaml
kubectl get serviceaccounts default -o yaml >./sa.yaml
kubectl replace serviceaccount default -f ./sa.yaml
```

资源名称：serviceaccounts，缩写：sa (注意：原文此处缩写为 ev，应为 sa)

### Replica Sets

```bash
kubectl get rs
kubectl describe rs
kubectl get rs -o wide
kubectl get rs -o yaml
```

资源名称：replicasets，缩写：rs

### Roles

```bash
kubectl get roles --all-namespaces
kubectl get roles --all-namespaces -o yaml
```

### Secrets

```bash
kubectl get secrets
kubectl get secrets --all-namespaces
kubectl get secrets -o yaml
```

### Config maps

资源名称：configmaps，缩写：cm

```bash
kubectl get cm
kubectl get cm --all-namespaces
kubectl get cm --all-namespaces -o yaml
```

### Ingresses

资源名称：ingresses，缩写：ing

```bash
kubectl get ing
kubectl get ing --all-namespaces
```

### Persistent Volumes

资源名称：persistentvolumes，缩写：pv

```bash
kubectl get pv
kubectl describe pv
```

### Persistent volume declaration

资源名称：persistentvolumeclaims，缩写：pvc

```bash
kubectl get pvc
kubectl describe pvc
```

### storage class

资源名称：storageclasses，缩写：sc

```bash
kubectl get sc
kubectl get sc -o yaml
```

### 多种资源

```bash
kubectl get svc, po
kubectl get deploy, no
kubectl get all
kubectl get all --all-namespaces
```

## 更新资源

### 污点

```bash
kubectl taint [node_name] [taint_name]
```

### 标签

```bash
kubectl label [node_name] disktype=ssd
kubectl label [pod_name] env=prod
```

### 维护/可调度

```bash
kubectl cordon [node_name] # 节点维护
kubectl uncordon [node_name] # 节点可调度
```

### 清空

```bash
kubectl drain [node_name] # 清空节点
```

### 节点/Pod {.row-span-2}

```bash
kubectl delete node [node_name]
kubectl delete pod [pod_name]
kubectl edit node [node_name]
kubectl edit pod [pod_name]
```

### 无状态/命名空间 {.row-span-2}

```bash
kubectl edit deploy [deploy_name]
kubectl delete deploy [deploy_name]
kubectl expose deploy [deploy_name] --port=80 --type=NodePort
kubectl scale deploy [deploy_name] --replicas=5
kubectl delete ns
kubectl edit ns [ns_name]
```

### Service

```bash
kubectl edit svc [svc_name]
kubectl delete svc [svc_name]
```

### Daemon set

```bash
kubectl edit ds [ds_name] -n kube-system
kubectl delete ds [ds_name]
```

### 服务账户

```bash
kubectl edit sa [sa_name]
kubectl delete sa [sa_name]
```

### 注解

```bash
kubectl annotate po [pod_name] [annotation]
kubectl annotateno [node_name]
```

## 创建资源

### 创建 pod

```bash
kubectl create -f [name_of_file]
kubectl apply -f [name_of_file]
kubectl run [pod_name] --image=nginx --restart=Never
kubectl run [pod_name] --generator=run-pod/v1 --image=nginx
kubectl run [pod_name] --image=nginx --restart=Never
```

### 创建 Service

```bash
kubectl create svc nodeport [svc_name] --tcp=8080:80
```

### 创建无状态应用

```bash
kubectl create -f [name_of_file]
kubectl apply -f [name_of_file]
kubectl create deploy [deploy_name] --image=nginx
```

### 交互

```bash
kubectl run [pod_name] --image=busybox --rm -it --restart=Never --sh
```

### 输出 YAML

```bash
kubectl create deploy [deploy_name] --image=nginx --dry-run -o yaml > deploy.yaml
kubectl get po [pod_name] -o yaml --export > pod.yaml
```

### 帮助

```bash
kubectl -h
kubectl create -h
kubectl run -h
kubectl explain deploy.spec
```

## 其他

### API

```bash
kubectl get --raw /apis/metrics.k8s.io/
```

### 信息

```bash
kubectl config
kubectl cluster-info
kubectl get componentstatus
```

## 另请参阅

- [Kubernetes 官方文档](https://kubernetes.io/zh-cn/docs/reference/kubectl/) _(kubernetes.io)_
