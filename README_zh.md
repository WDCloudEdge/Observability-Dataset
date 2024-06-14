# MicroCERCL

## 简介

云边协同环境中基于混合部署的微服务系统的可观测性数据集。

## 数据集

### 下载链接

[Dropbox](https://www.dropbox.com/scl/fi/s6gugabhlfd4ar46vu3nf/abnormal.zip?rlkey=iztl9kqkorakqt6dxocmlv3k7&st=jsbbcozk&dl=0)

### 数据集描述

包含三个文件夹，分别对应混合部署场景中故障根因所在的 Bookinfo、Hipster 和 SockShop系统。根据不同的微服务（或其实例）故障原因，每个文件夹被进一步拆分为二级文件夹。每个根因服务文件夹都包含注入的所有故障的标签信息（xxx_label.txt）。在每个服务中，根据标签文件将其拆分为三级文件夹，形成故障样本。每个故障样本包含所有混合部署的微服务系统数据，构成第四级文件夹。每个混合部署的微服务系统文件夹包含三种类型的监控数据：指标、跟踪和日志（ Bookinfo中的每个故障样本不含日志数据）。
如图所示:

<img width="310" alt="image" src="https://github.com/WDCloudEdge/MicroCERCL/assets/48899336/461ec9a0-80c9-4fb1-a989-566cb14661e6">

### 故障样本

当发生故障时，一个故障样本包含混合部署的微服务系统的所有监控数据。
如图所示:

<img width="324" alt="image" src="https://github.com/WDCloudEdge/MicroCERCL/assets/48899336/346c2b81-371b-41ca-92de-ce99df51509e">

### 数据细节

#### Metrics

<img width="193" alt="image" src="https://github.com/WDCloudEdge/MicroCERCL/assets/48899336/6b7e5e22-0d5d-4629-9dbe-ca09c5894766">

| File             | Description                                                                                                                                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| call.csv         | Time-series call latency between microservices is denoted by P99, P95, and P90, which denote the 99th, 95th, and 90th percentiles of the latency data.                                                                  |
| graph.csv        | Time-series topologies denote the instance, the server where it is located, and the service call link.                                                                                                                  |
| instance.csv     | Time-series metrics of each instance, containing CPU usage, memory usage, and network transmit packets.                                                                                                                 |
| latency.csv      | The time-series latency of microservices is denoted by P99, P95, and P90, which denote the 99th, 95th, and 90th percentiles of the latency data.                                                                        |
| resource.csv     | Time-series metrics of instances within a specific namespace, containing the total CPU usage and memory usage                                                                                                           |
| success_rate.csv | Time-series success rate of microservices                                                                                                                                                                               |
| svc_metric.csv   | Time-series metrics of microservices (the average of its instances), containing CPU usage, CPU limit, memory usage, memory limit, FS write, FS read, FS usage, net receive, net transmit, and network transmit packets. |
| svc_qps.csv      | 微服务qps时序数据                                                                                                                                                                                                              |

#### Traces

<img width="217" alt="image" src="https://github.com/WDCloudEdge/MicroCERCL/assets/48899336/6ab3177b-3502-413c-b77f-4251387a3d20">

#### Logs

每个实例（容器）都有一个 .pkl 文件，其中包含容器的所有业务日志。<img width="301" alt="image" src="https://github.com/WDCloudEdge/MicroCERCL/assets/48899336/e3bddbcf-8b6e-4b02-8f9c-1cbd6945cb43">

## 项目结构

```textile

```
