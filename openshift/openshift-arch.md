# OpenShift架构

本文参照`<<OpenShift Container Platform 3.11 Architecture>>`.



## OpenShift是什么

> OpenShift v3 is a layered system designed to expose underlying Docker-formatted container image and Kubernetes concepts as accurately as possible, with a focus on easy composition of applications by a developer. For example, install Ruby, push code, and add MySQL.
> Unlike OpenShift v2, more flexibility of configuration is exposed after creation in all aspects of the model. The concept of an application as a separate object is removed in favor of more flexible composition of "services", allowing two web containers to reuse a database or expose a database directly to the edge of the network.


**什么是分层?**

Docker服务提供了基于linux轻量级镜像的打包创建能力的抽象。kubernetes提供了集群的管理能力和跨主机容器编排能力。openshift提供了：

1. 为开发者提供源码管理，构建部署
2. 

### layers是什么
### openshift container platform 架构
### openshift container如何电镀的

## infrastructure components

### kubeneters基础设施

### 容器registry
### web console

## 核心该你那
### overview
### containers and images
### pods and services
### projects and users
### builds and images streams
### deployments
### templates

## additional concepts
### authentication
### authorization
### persistent storage
### ephemeeral local storage
### source control management
### admission controllers
### custom admission controllers
### other api objects

## 网络
### openshift SDN
### sdn plugin-ins
### router plugin-ins
### port forwarding
### remote commands
### routes

## service catalog components
### service catalog
### service catalog command-line interface
### template service broker
### openshift ansible broker

