[![Build Status](https://travis-ci.org/kubernetes-sigs/kubefed.svg?branch=master)](https://travis-ci.org/kubernetes-sigs/kubefed "Travis")
[![Go Report Card](https://goreportcard.com/badge/github.com/kubernetes-sigs/kubefed)](https://goreportcard.com/report/github.com/kubernetes-sigs/kubefed)
[![Image Repository on Quay](https://quay.io/repository/kubernetes-multicluster/kubefed/status "Image Repository on Quay")](https://quay.io/repository/kubernetes-multicluster/kubefed)
[![LICENSE](https://img.shields.io/badge/license-apache2.0-green.svg)](https://github.com/kubernetes-sigs/kubefed/blob/master/LICENSE)
[![Releases](https://img.shields.io/github/release/kubernetes-sigs/kubefed/all.svg)](https://github.com/kubernetes-sigs/kubefed/releases "KubeFed latest release")

# Kubernetes集群联邦

Kubernetes集群联邦(简称KubeFed)允许您使用托管集群中的一组API，来协调多个Kubernetes集群的配置。KubeFed的目标是提供一种机制，用于表示哪些集群的配置应该被管理以及那些配置应该是什么样的。KubeFed提供的机制是底层的，旨在为部署跨地区的应用和灾难恢复等复杂的多集群场景奠定基础。

KubeFed目前是**alpha版本**，并正在迅速向[beta版本](https://github.com/kubernetes-sigs/kubefed/milestone/4)演进。

## 概念

<p align="center"><img src="docs/images/concepts.png" width="711"></p>

KubeFed配置了两种类型的信息:

- **Type configuration（类型配置）** 声明KubeFed应该处理哪些API类型
- **Cluster configuration（集群配置）** 声明KubeFed应该针对哪些集群

**Propagation（传播）**指的是将资源分配到联邦集群的机制。

类型配置有三个基本概念:

- **Templates（模板）** 定义跨集群的公共资源的表示形式
- **Placement（放置）** 定义资源将出现在哪些集群中
- **Overrides（重写）** 定义每个集群字段级别的变体以应用于模板

这三者抽象提供了计划出现在多个集群中资源的简单表示。它们编码了**传播**所需的最小信息，非常适合充当 任何给定传播机制 与 类似基于策略的放置和动态调度等高阶行为之间的粘合剂。

这些基本概念提供了可被高层API使用的积木:

- **Status（状态）**收集KubeFed跨所有联合集群分发资源的状态
- **Policy（策略）**确定一个资源可以分配到集群的哪个子集
- **Scheduling（调度）**指的是一种决策能力，它可以决定工作负载应该如何分布在不同的集群中，类似于人工操作的方式

## 特性

| 特性 | 成熟度 | 特性门类 | 默认 |
|---------|----------|--------------|---------|
| [任意类型到远程集群的推送传播](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/userguide.md#verify-your-deployment-is-working) | Alpha | PushReconciler | 是 |
| [CLI 有效性 (`kubefedctl`)](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/userguide.md#kubefedctl-cli) | Alpha | | |
| [无需编写代码即可生成KubeFed API](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/userguide.md#enabling-federation-of-an-api-type) | Alpha | | |
| [通过 `external-dns` 实现多集群服务DNS](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/servicedns-with-externaldns.md) | Alpha | CrossClusterServiceDiscovery | 是 |
| [通过 `external-dns` 实现多集群入口DNS](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/ingressdns-with-externaldns.md) | Alpha | FederatedIngress | 是 |
| [复制调度偏好](https://github.com/kubernetes-sigs/kubefed/blob/master/docs/userguide.md#replicaschedulingpreference) | Alpha | SchedulerPreferences | 是 |

## 指南

### 用户指南

如果你对于使用KubeFed感兴趣，请参阅我们的 [用户指南](docs/userguide.md)。

### 开发指南

如果你对于贡献KubeFed感兴趣，请参阅我们的 [开发指南](docs/development.md)。

## 社区

如果你想贡献KubeFed，请参阅我们的 [贡献指南](./CONTRIBUTING.md) if you would like to contribute to KubeFed.

### 沟通渠道

KubeFed是由[SIG Multicluster](https://github.com/kubernetes/community/tree/master/sig-multicluster)赞助的，它使用与SIG multicluster相同的通信通道。

* Slack 频道: [#sig-multicluster](http://slack.k8s.io/#sig-multicluster)
* [邮件列表](https://groups.google.com/forum/#!forum/kubernetes-sig-multicluster)

## 行为准则

参与Kubernetes社区需要遵守 [Kubernetes行为准则](./code-of-conduct.md)的管理。
