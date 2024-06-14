# Observability Dataset
[中文文档](README_zh.md)

## Description

Observability datasets of hybrid-deployed microservice systems in the cloud-edge collaborative environment.

## Dataset

### Download

[Dropbox](https://www.dropbox.com/scl/fi/s6gugabhlfd4ar46vu3nf/abnormal.zip?rlkey=iztl9kqkorakqt6dxocmlv3k7&st=jsbbcozk&dl=0)

### Folder Structure

It contains three folders corresponding to Bookinfo, Hipster, and SockShop, where the root cause is located within a hybrid deployment scenario. Each folder is further split into secondary folders based on the root cause of the microservice (or its instances). Each root cause service folder contains label information (xxx_label.txt) for all failures injected. Within each service, it is split into third-level folders according to the label file to form a failure sample. Each failure sample contains all hybrid-deployed microservice systems that form the fourth-level folders. Each hybrid-deployed microservice system folder contains three types of monitoring data: metrics, traces, and logs (Bookinfo without logs in each failure sample).
As shown in figure:

<img width="310" alt="image" src="https://github.com/WDCloudEdge/MicroCERCL/assets/48899336/461ec9a0-80c9-4fb1-a989-566cb14661e6">

### Failure Sample

It contains all the monitoring data of hybrid-deployed microservice systems when a failure occurs.
As shown in figure:

<img width="324" alt="image" src="https://github.com/WDCloudEdge/MicroCERCL/assets/48899336/346c2b81-371b-41ca-92de-ce99df51509e">

### Details

#### Metrics

<img width="193" alt="image" src="https://github.com/WDCloudEdge/MicroCERCL/assets/48899336/6b7e5e22-0d5d-4629-9dbe-ca09c5894766">

| File             | Description                                                                                                                                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| call.csv         | Time-series call latency between microservices, including P99, P95, and P90, which denote the 99th, 95th, and 90th percentiles of the latency data.                                                                     |
| graph.csv        | Time-series topologies contain the instance, the server where it is located, and the service call relationship.                                                                                                         |
| instance.csv     | Time-series metrics of each instance, containing CPU usage, memory usage, and network transmit packets.                                                                                                                 |
| latency.csv      | The time-series latency of microservices, including P99, P95, and P90, which denote the 99th, 95th, and 90th percentiles of the latency data.                                                                           |
| resource.csv     | Time-series metrics of instances within a specific namespace, containing the total CPU usage and memory usage                                                                                                           |
| success_rate.csv | Microservice Success Rate Time Series Data                                                                                                                                                                              |
| svc_metric.csv   | Time-series metrics of microservices (the average of its instances), containing CPU usage, CPU limit, memory usage, memory limit, FS write, FS read, FS usage, net receive, net transmit, and network transmit packets. |
| svc_qps.csv      | Microservice QPS (Queries Per Second) Time Series Data                                                                                                                                                                  |

#### Traces

<img width="217" alt="image" src="https://github.com/WDCloudEdge/MicroCERCL/assets/48899336/6ab3177b-3502-413c-b77f-4251387a3d20">

| File                  | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| abnormal.pkl          | Records data with missing structure, abnormal status code and error messages, excluding data with abnormal net latency. |
| abnormal_half.pkl     | For the namespace where the file is located, records data after eliminating other namespace service information from the Trace data based on *abnormal.pkl* (only this namespace service information is included) |
| inbound.pkl           | For the namespace where the file is located, record data containing service calls from other namespaces to this namespace. |
| inbound_half.pkl      | For the namespace where the file is located, records data after eliminating other namespace service information from the Trace data based on *inbound.pkl* (only this namespace service information is included) |
| normal.pkl            | Records data with complete structure and normal status code, including data with abnormal net latency. |
| outbound.pkl          | For the namespace where the file is located, record data containing service calls from this namespace to other namespaces. |
| outbound_half.pkl     | For the namespace where the file is located, records data after eliminating other namespace service information from the Trace data based on *outbound.pkl* (only this namespace service information is included) |
| trace_net_latency.pkl | Statistics on request latency data and response latency data between a pair of service calls |
| trace_pod_latency.pkl | Statistics on latency data between sending a request and receiving a response between a pair of service calls. |

#### Logs

Each instance (container) has a .pkl file, containing all business logs of the container.

<img width="301" alt="image" src="https://github.com/WDCloudEdge/MicroCERCL/assets/48899336/e3bddbcf-8b6e-4b02-8f9c-1cbd6945cb43">

## Dataset Structure

```textile
abnormal/
│├── bookinfo_chaos/
│├── │├── details/
│├── │├── │├── cloud_pod_details_cpu_1/
│├── │├── │├── cloud_pod_details_cpu_2/
│├── │├── │├── cloud_pod_details_cpu_3/
│├── │├── │├── cloud_pod_details_cpu_4/
│├── │├── │├── cloud_pod_details_cpu_5/
│├── │├── │├── cloud_pod_details_cpu_6/
│├── │├── │├── cloud_pod_details_cpu_7/
│├── │├── │├── cloud_pod_details_cpu_8/
│├── │├── │├── cloud_pod_details_mem_1/
│├── │├── │├── cloud_pod_details_mem_2/
│├── │├── │├── cloud_pod_details_mem_3/
│├── │├── │├── cloud_pod_details_mem_4/
│├── │├── │├── cloud_pod_details_mem_5/
│├── │├── │├── cloud_pod_details_mem_6/
│├── │├── │├── cloud_pod_details_mem_7/
│├── │├── │├── cloud_pod_details_net_1/
│├── │├── │├── cloud_pod_details_net_2/
│├── │├── │├── cloud_pod_details_net_3/
│├── │├── │├── cloud_pod_details_net_4/
│├── │├── │├── cloud_pod_details_net_5/
│├── │├── │├── cloud_pod_details_net_6/
│├── │├── │└── details_label.txt
│├── │├── details-v1-edge/
│├── │├── │├── details-v1-edge_label.txt
│├── │├── │├── edge_pod_details-v1-edge_cpu_1/
│├── │├── │├── edge_pod_details-v1-edge_cpu_2/
│├── │├── │├── edge_pod_details-v1-edge_cpu_3/
│├── │├── │├── edge_pod_details-v1-edge_cpu_4/
│├── │├── │├── edge_pod_details-v1-edge_cpu_5/
│├── │├── │├── edge_pod_details-v1-edge_cpu_6/
│├── │├── │├── edge_pod_details-v1-edge_cpu_7/
│├── │├── │├── edge_pod_details-v1-edge_cpu_8/
│├── │├── │├── edge_pod_details-v1-edge_mem_1/
│├── │├── │├── edge_pod_details-v1-edge_mem_2/
│├── │├── │├── edge_pod_details-v1-edge_mem_3/
│├── │├── │├── edge_pod_details-v1-edge_mem_5/
│├── │├── │├── edge_pod_details-v1-edge_mem_6/
│├── │├── │├── edge_pod_details-v1-edge_mem_7/
│├── │├── │├── edge_pod_details-v1-edge_mem_8/
│├── │├── │├── edge_pod_details-v1-edge_net_1/
│├── │├── │├── edge_pod_details-v1-edge_net_2/
│├── │├── │├── edge_pod_details-v1-edge_net_3/
│├── │├── │├── edge_pod_details-v1-edge_net_4/
│├── │├── │├── edge_pod_details-v1-edge_net_5/
│├── │├── │├── edge_pod_details-v1-edge_net_6/
│├── │├── │├── edge_pod_details-v1-edge_net_7/
│├── │├── │└── edge_pod_details-v1-edge_net_8/
│├── │├── productpage/
│├── │├── │├── cloud_pod_productpage_cpu_1/
│├── │├── │├── cloud_pod_productpage_cpu_2/
│├── │├── │├── cloud_pod_productpage_cpu_3/
│├── │├── │├── cloud_pod_productpage_cpu_4/
│├── │├── │├── cloud_pod_productpage_cpu_5/
│├── │├── │├── cloud_pod_productpage_cpu_6/
│├── │├── │├── cloud_pod_productpage_cpu_7/
│├── │├── │├── cloud_pod_productpage_cpu_8/
│├── │├── │├── cloud_pod_productpage_mem_1/
│├── │├── │├── cloud_pod_productpage_mem_10/
│├── │├── │├── cloud_pod_productpage_mem_11/
│├── │├── │├── cloud_pod_productpage_mem_12/
│├── │├── │├── cloud_pod_productpage_mem_13/
│├── │├── │├── cloud_pod_productpage_mem_14/
│├── │├── │├── cloud_pod_productpage_mem_15/
│├── │├── │├── cloud_pod_productpage_mem_16/
│├── │├── │├── cloud_pod_productpage_mem_17/
│├── │├── │├── cloud_pod_productpage_mem_18/
│├── │├── │├── cloud_pod_productpage_mem_19/
│├── │├── │├── cloud_pod_productpage_mem_2/
│├── │├── │├── cloud_pod_productpage_mem_20/
│├── │├── │├── cloud_pod_productpage_mem_21/
│├── │├── │├── cloud_pod_productpage_mem_22/
│├── │├── │├── cloud_pod_productpage_mem_3/
│├── │├── │├── cloud_pod_productpage_mem_4/
│├── │├── │├── cloud_pod_productpage_mem_5/
│├── │├── │├── cloud_pod_productpage_mem_6/
│├── │├── │├── cloud_pod_productpage_mem_7/
│├── │├── │├── cloud_pod_productpage_mem_8/
│├── │├── │├── cloud_pod_productpage_mem_9/
│├── │├── │├── cloud_pod_productpage_net_1/
│├── │├── │├── cloud_pod_productpage_net_2/
│├── │├── │├── cloud_pod_productpage_net_3/
│├── │├── │├── cloud_pod_productpage_net_4/
│├── │├── │├── cloud_pod_productpage_net_5/
│├── │├── │├── cloud_pod_productpage_net_6/
│├── │├── │├── cloud_pod_productpage_net_7/
│├── │├── │├── cloud_pod_productpage_net_8/
│├── │├── │└── productpage_label.txt
│├── │├── ratings/
│├── │├── │├── cloud_pod_ratings_cpu_1/
│├── │├── │├── cloud_pod_ratings_cpu_2/
│├── │├── │├── cloud_pod_ratings_cpu_3/
│├── │├── │├── cloud_pod_ratings_cpu_4/
│├── │├── │├── cloud_pod_ratings_cpu_5/
│├── │├── │├── cloud_pod_ratings_mem_1/
│├── │├── │├── cloud_pod_ratings_mem_2/
│├── │├── │├── cloud_pod_ratings_mem_3/
│├── │├── │├── cloud_pod_ratings_mem_4/
│├── │├── │├── cloud_pod_ratings_mem_5/
│├── │├── │├── cloud_pod_ratings_net_1/
│├── │├── │├── cloud_pod_ratings_net_2/
│├── │├── │├── cloud_pod_ratings_net_3/
│├── │├── │├── cloud_pod_ratings_net_4/
│├── │├── │├── cloud_pod_ratings_net_5/
│├── │├── │└── ratings_label.txt
│├── │├── ratings-v1-edge/
│├── │├── │├── edge_pod_ratings-v1-edge_cpu_1/
│├── │├── │├── edge_pod_ratings-v1-edge_cpu_2/
│├── │├── │├── edge_pod_ratings-v1-edge_cpu_3/
│├── │├── │├── edge_pod_ratings-v1-edge_cpu_4/
│├── │├── │├── edge_pod_ratings-v1-edge_cpu_5/
│├── │├── │├── edge_pod_ratings-v1-edge_mem_1/
│├── │├── │├── edge_pod_ratings-v1-edge_mem_2/
│├── │├── │├── edge_pod_ratings-v1-edge_mem_3/
│├── │├── │├── edge_pod_ratings-v1-edge_mem_4/
│├── │├── │├── edge_pod_ratings-v1-edge_mem_5/
│├── │├── │├── edge_pod_ratings-v1-edge_net_1/
│├── │├── │├── edge_pod_ratings-v1-edge_net_2/
│├── │├── │├── edge_pod_ratings-v1-edge_net_3/
│├── │├── │├── edge_pod_ratings-v1-edge_net_4/
│├── │├── │├── edge_pod_ratings-v1-edge_net_5/
│├── │├── │└── ratings-v1-edge_label.txt
│├── │├── reviews-v1/
│├── │├── │├── cloud_pod_reviews-v1_cpu_1/
│├── │├── │├── cloud_pod_reviews-v1_cpu_2/
│├── │├── │├── cloud_pod_reviews-v1_cpu_3/
│├── │├── │├── cloud_pod_reviews-v1_cpu_4/
│├── │├── │├── cloud_pod_reviews-v1_cpu_5/
│├── │├── │├── cloud_pod_reviews-v1_cpu_6/
│├── │├── │├── cloud_pod_reviews-v1_cpu_7/
│├── │├── │├── cloud_pod_reviews-v1_cpu_8/
│├── │├── │├── cloud_pod_reviews-v1_mem_1/
│├── │├── │├── cloud_pod_reviews-v1_mem_2/
│├── │├── │├── cloud_pod_reviews-v1_mem_3/
│├── │├── │├── cloud_pod_reviews-v1_mem_4/
│├── │├── │├── cloud_pod_reviews-v1_mem_5/
│├── │├── │├── cloud_pod_reviews-v1_mem_6/
│├── │├── │├── cloud_pod_reviews-v1_net_1/
│├── │├── │├── cloud_pod_reviews-v1_net_2/
│├── │├── │├── cloud_pod_reviews-v1_net_3/
│├── │├── │├── cloud_pod_reviews-v1_net_4/
│├── │├── │├── cloud_pod_reviews-v1_net_5/
│├── │├── │├── cloud_pod_reviews-v1_net_6/
│├── │├── │├── cloud_pod_reviews-v1_net_7/
│├── │├── │├── cloud_pod_reviews-v1_net_8/
│├── │├── │└── reviews-v1_label.txt
│├── │├── reviews-v1-edge/
│├── │├── │├── edge_pod_reviews-v1-edge_cpu_1/
│├── │├── │├── edge_pod_reviews-v1-edge_cpu_2/
│├── │├── │├── edge_pod_reviews-v1-edge_cpu_3/
│├── │├── │├── edge_pod_reviews-v1-edge_cpu_4/
│├── │├── │├── edge_pod_reviews-v1-edge_cpu_5/
│├── │├── │├── edge_pod_reviews-v1-edge_mem_1/
│├── │├── │├── edge_pod_reviews-v1-edge_mem_2/
│├── │├── │├── edge_pod_reviews-v1-edge_mem_3/
│├── │├── │├── edge_pod_reviews-v1-edge_mem_4/
│├── │├── │├── edge_pod_reviews-v1-edge_mem_5/
│├── │├── │├── edge_pod_reviews-v1-edge_net_1/
│├── │├── │├── edge_pod_reviews-v1-edge_net_2/
│├── │├── │├── edge_pod_reviews-v1-edge_net_3/
│├── │├── │├── edge_pod_reviews-v1-edge_net_4/
│├── │├── │└── reviews-v1-edge_label.txt
│├── │├── reviews-v2/
│├── │├── │├── cloud_pod_reviews-v2_cpu_1/
│├── │├── │├── cloud_pod_reviews-v2_cpu_2/
│├── │├── │├── cloud_pod_reviews-v2_cpu_3/
│├── │├── │├── cloud_pod_reviews-v2_cpu_4/
│├── │├── │├── cloud_pod_reviews-v2_cpu_5/
│├── │├── │├── cloud_pod_reviews-v2_cpu_6/
│├── │├── │├── cloud_pod_reviews-v2_cpu_7/
│├── │├── │├── cloud_pod_reviews-v2_cpu_8/
│├── │├── │├── cloud_pod_reviews-v2_mem_1/
│├── │├── │├── cloud_pod_reviews-v2_mem_2/
│├── │├── │├── cloud_pod_reviews-v2_mem_3/
│├── │├── │├── cloud_pod_reviews-v2_mem_4/
│├── │├── │├── cloud_pod_reviews-v2_mem_5/
│├── │├── │├── cloud_pod_reviews-v2_mem_6/
│├── │├── │├── cloud_pod_reviews-v2_mem_7/
│├── │├── │├── cloud_pod_reviews-v2_mem_8/
│├── │├── │├── cloud_pod_reviews-v2_net_1/
│├── │├── │├── cloud_pod_reviews-v2_net_2/
│├── │├── │├── cloud_pod_reviews-v2_net_3/
│├── │├── │├── cloud_pod_reviews-v2_net_4/
│├── │├── │├── cloud_pod_reviews-v2_net_5/
│├── │├── │├── cloud_pod_reviews-v2_net_6/
│├── │├── │├── cloud_pod_reviews-v2_net_7/
│├── │├── │├── cloud_pod_reviews-v2_net_8/
│├── │├── │└── reviews-v2_label.txt
│├── │├── reviews-v2-edge/
│├── │├── │├── edge_pod_reviews-v2-edge_cpu_1/
│├── │├── │├── edge_pod_reviews-v2-edge_cpu_2/
│├── │├── │├── edge_pod_reviews-v2-edge_cpu_3/
│├── │├── │├── edge_pod_reviews-v2-edge_cpu_4/
│├── │├── │├── edge_pod_reviews-v2-edge_cpu_5/
│├── │├── │├── edge_pod_reviews-v2-edge_mem_1/
│├── │├── │├── edge_pod_reviews-v2-edge_mem_2/
│├── │├── │├── edge_pod_reviews-v2-edge_mem_3/
│├── │├── │├── edge_pod_reviews-v2-edge_mem_4/
│├── │├── │├── edge_pod_reviews-v2-edge_mem_5/
│├── │├── │├── edge_pod_reviews-v2-edge_net_1/
│├── │├── │├── edge_pod_reviews-v2-edge_net_2/
│├── │├── │├── edge_pod_reviews-v2-edge_net_3/
│├── │├── │├── edge_pod_reviews-v2-edge_net_4/
│├── │├── │├── edge_pod_reviews-v2-edge_net_5/
│├── │├── │└── reviews-v2-edge_label.txt
│├── │├── reviews-v3/
│├── │├── │├── cloud_pod_reviews-v3_cpu_1/
│├── │├── │├── cloud_pod_reviews-v3_cpu_2/
│├── │├── │├── cloud_pod_reviews-v3_cpu_3/
│├── │├── │├── cloud_pod_reviews-v3_cpu_4/
│├── │├── │├── cloud_pod_reviews-v3_cpu_5/
│├── │├── │├── cloud_pod_reviews-v3_mem_1/
│├── │├── │├── cloud_pod_reviews-v3_mem_2/
│├── │├── │├── cloud_pod_reviews-v3_mem_3/
│├── │├── │├── cloud_pod_reviews-v3_mem_4/
│├── │├── │├── cloud_pod_reviews-v3_mem_5/
│├── │├── │├── cloud_pod_reviews-v3_net_1/
│├── │├── │├── cloud_pod_reviews-v3_net_2/
│├── │├── │├── cloud_pod_reviews-v3_net_3/
│├── │├── │├── cloud_pod_reviews-v3_net_4/
│├── │├── │├── cloud_pod_reviews-v3_net_5/
│├── │├── │└── reviews-v3_label.txt
│├── │└── reviews-v3-edge/
│├── │└── │├── edge_pod_reviews-v3-edge_cpu_1/
│├── │└── │├── edge_pod_reviews-v3-edge_cpu_2/
│├── │└── │├── edge_pod_reviews-v3-edge_cpu_3/
│├── │└── │├── edge_pod_reviews-v3-edge_cpu_4/
│├── │└── │├── edge_pod_reviews-v3-edge_cpu_5/
│├── │└── │├── edge_pod_reviews-v3-edge_mem_1/
│├── │└── │├── edge_pod_reviews-v3-edge_mem_2/
│├── │└── │├── edge_pod_reviews-v3-edge_mem_3/
│├── │└── │├── edge_pod_reviews-v3-edge_mem_4/
│├── │└── │├── edge_pod_reviews-v3-edge_mem_5/
│├── │└── │└── reviews-v3-edge_label.txt
│├── hipster_chaos/
│├── │├── adservice/
│├── │├── │├── adservice_label.txt
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_cpu_10/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_cpu_6/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_cpu_7/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_cpu_8/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_cpu_9/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_mem_10/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_mem_6/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_mem_7/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_mem_8/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_mem_9/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_net_10/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_net_6/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_net_7/
│├── │├── │├── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_net_8/
│├── │├── │└── cloud_pod_adservice_adservice-5459b9d5f7-mnbsd_net_9/
│├── │├── adservice-edge/
│├── │├── │├── adservice-edge_label.txt
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_cpu_10/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_cpu_6/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_cpu_7/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_cpu_8/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_cpu_9/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_mem_10/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_mem_6/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_mem_7/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_mem_8/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_mem_9/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_net_10/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_net_6/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_net_7/
│├── │├── │├── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_net_8/
│├── │├── │└── edge-2_pod_adservice-edge_adservice-edge-5bbc6577c-h7dbd_net_9/
│├── │├── cartservice/
│├── │├── │├── cartservice_label.txt
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_cpu_10/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_cpu_6/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_cpu_7/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_cpu_8/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_cpu_9/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_mem_10/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_mem_6/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_mem_7/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_mem_8/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_mem_9/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_net_10/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_net_6/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_net_7/
│├── │├── │├── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_net_8/
│├── │├── │└── cloud_pod_cartservice_cartservice-bc7d76455-f9rwj_net_9/
│├── │├── cartservice-edge/
│├── │├── │├── cartservice-edge_label.txt
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_cpu_10/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_cpu_6/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_cpu_7/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_cpu_8/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_cpu_9/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_mem_10/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_mem_6/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_mem_7/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_mem_8/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_mem_9/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_net_10/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_net_6/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_net_7/
│├── │├── │├── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_net_8/
│├── │├── │└── edge-2_pod_cartservice-edge_cartservice-edge-58f487459d-nnjcv_net_9/
│├── │├── checkoutservice/
│├── │├── │├── checkoutservice_label.txt
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_cpu_10/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_cpu_6/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_cpu_7/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_cpu_8/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_cpu_9/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_mem_10/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_mem_6/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_mem_7/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_mem_8/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_mem_9/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_net_10/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_net_6/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_net_7/
│├── │├── │├── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_net_8/
│├── │├── │└── cloud_pod_checkoutservice_checkoutservice-799957b559-l2zg8_net_9/
│├── │├── currencyservice/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_cpu_10/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_cpu_6/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_cpu_7/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_cpu_8/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_cpu_9/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_mem_10/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_mem_6/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_mem_7/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_mem_8/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_mem_9/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_net_10/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_net_6/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_net_7/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_net_8/
│├── │├── │├── cloud_pod_currencyservice_currencyservice-6b65476b59-mgbkn_net_9/
│├── │├── │└── currencyservice_label.txt
│├── │├── currencyservice-edge/
│├── │├── │├── currencyservice-edge_label.txt
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_cpu_10/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_cpu_6/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_cpu_7/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_cpu_8/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_cpu_9/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_mem_10/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_mem_6/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_mem_7/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_mem_8/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_mem_9/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_net_10/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_net_6/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_net_7/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_net_8/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-9pmc8_net_9/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_cpu_1/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_cpu_2/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_cpu_3/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_cpu_4/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_cpu_5/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_mem_1/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_mem_2/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_mem_3/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_mem_4/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_mem_5/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_net_1/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_net_2/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_net_3/
│├── │├── │├── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_net_4/
│├── │├── │└── edge-2_pod_currencyservice-edge_currencyservice-edge-745869c69d-lpx4g_net_5/
│├── │├── emailservice/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_cpu_10/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_cpu_6/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_cpu_7/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_cpu_8/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_cpu_9/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_mem_10/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_mem_6/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_mem_7/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_mem_8/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_mem_9/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_net_10/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_net_6/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_net_7/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_net_8/
│├── │├── │├── cloud_pod_emailservice_emailservice-5cbf55c5b4-2jjrz_net_9/
│├── │├── │└── emailservice_label.txt
│├── │├── emailservice-edge/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_cpu_10/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_cpu_6/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_cpu_7/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_cpu_8/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_cpu_9/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_mem_10/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_mem_6/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_mem_7/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_mem_8/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_mem_9/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_net_10/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_net_6/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_net_7/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_net_8/
│├── │├── │├── edge-2_emailservice-edge_emailservice-edge-5648d99fff-cdghx_net_9/
│├── │├── │└── emailservice-edge_label.txt
│├── │├── frontend/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_cpu_10/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_cpu_6/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_cpu_7/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_cpu_8/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_cpu_9/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_mem_10/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_mem_6/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_mem_7/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_mem_8/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_mem_9/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_net_10/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_net_6/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_net_7/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_net_8/
│├── │├── │├── cloud_pod_frontend_frontend-64d8986cf8-6jm6g_net_9/
│├── │├── │└── frontend_label.txt
│├── │├── paymentservice/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_cpu_10/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_cpu_6/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_cpu_7/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_cpu_8/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_cpu_9/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_mem_10/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_mem_6/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_mem_7/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_mem_8/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_mem_9/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_net_10/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_net_6/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_net_7/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_net_8/
│├── │├── │├── cloud_pod_paymentservice_paymentservice-6b9dbbc87d-28hwm_net_9/
│├── │├── │└── paymentservice_label.txt
│├── │├── paymentservice-edge/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_cpu_10/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_cpu_6/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_cpu_7/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_cpu_8/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_cpu_9/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_mem_10/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_mem_6/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_mem_7/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_mem_8/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_mem_9/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_net_10/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_net_6/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_net_7/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_net_8/
│├── │├── │├── edge-2_pod_paymentservice-edge_paymentservice-edge-6d455469d7-5gbwq_net_9/
│├── │├── │└── paymentservice-edge_label.txt
│├── │├── productcatalogservice/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_cpu_10/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_cpu_6/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_cpu_7/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_cpu_8/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_cpu_9/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_mem_10/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_mem_6/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_mem_7/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_mem_8/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_mem_9/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_net_10/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_net_6/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_net_7/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_net_8/
│├── │├── │├── cloud_pod_productcatalog_productcatalogservice-b6569dc96-q744q_net_9/
│├── │├── │└── productcatalogservice_label.txt
│├── │├── productcatalogservice-edge/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_cpu_10/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_cpu_6/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_cpu_7/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_cpu_8/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_cpu_9/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_mem_10/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_mem_6/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_mem_7/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_mem_8/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_mem_9/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_net_10/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_net_6/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_net_7/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_net_8/
│├── │├── │├── edge-2_pod_productcatalogservice-edge_productcatalogservice-edge-599c5894f9-c9ks2_net_9/
│├── │├── │└── productcatalogservice-edge_label.txt
│├── │├── recommendationservice/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_cpu_10/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_cpu_6/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_cpu_7/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_cpu_8/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_cpu_9/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_mem_10/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_mem_6/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_mem_7/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_mem_8/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_mem_9/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_net_10/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_net_6/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_net_7/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_net_8/
│├── │├── │├── cloud_pod_recommendationservice_recommendationservice-7595d86c4c-52j5l_net_9/
│├── │├── │└── recommendationservice_label.txt
│├── │├── recommendationservice-edge/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_cpu_10/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_cpu_6/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_cpu_7/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_cpu_8/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_cpu_9/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_mem_10/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_mem_6/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_mem_7/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_mem_8/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_mem_9/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_net_10/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_net_6/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_net_7/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_net_8/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-9jqwr_net_9/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_cpu_1/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_cpu_2/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_cpu_3/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_cpu_4/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_cpu_5/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_mem_1/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_mem_2/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_mem_3/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_mem_4/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_net_1/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_net_2/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_net_3/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_net_4/
│├── │├── │├── edge-2_pod_recommendationservice-edge_recommendationservice-edge-9b55f59d-jltqm_net_5/
│├── │├── │└── recommendationservice-edge_label.txt
│├── │├── shippingservice/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_cpu_10/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_cpu_6/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_cpu_7/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_cpu_8/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_cpu_9/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_mem_10/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_mem_6/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_mem_7/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_mem_8/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_mem_9/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_net_10/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_net_6/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_net_7/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_net_8/
│├── │├── │├── cloud_pod_shippingservice_shippingservice-545b594fd6-s47gc_net_9/
│├── │├── │└── shippingservice_label.txt
│├── │└── shippingservice-edge/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_cpu_10/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_cpu_6/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_cpu_7/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_cpu_8/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_cpu_9/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_mem_10/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_mem_6/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_mem_7/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_mem_8/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_mem_9/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_net_10/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_net_6/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_net_7/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_net_8/
│├── │└── │├── edge-2_pod_shippingservice_shippingservice-edge-c64bfd4fc-qzlg7_net_9/
│├── │└── │└── shippingservice-edge_label.txt
│└── sock_shop_chaos/
│└── │├── carts-cloud/
│└── │├── │├── carts-cloud_label.txt
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_cpu_1/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_cpu_10/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_cpu_2/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_cpu_3/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_cpu_4/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_cpu_5/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_cpu_6/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_cpu_7/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_cpu_8/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_cpu_9/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_mem_1/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_mem_10/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_mem_2/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_mem_3/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_mem_4/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_mem_5/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_mem_6/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_mem_7/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_mem_8/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_mem_9/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_net_1/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_net_10/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_net_2/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_net_3/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_net_4/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_net_5/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_net_6/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_net_7/
│└── │├── │├── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_net_8/
│└── │├── │└── cloud_pod_carts-cloud-xffvd_carts-cloud-xffvd-66b97fcd4-g7jmv_net_9/
│└── │├── carts-edge/
│└── │├── │├── carts-edge_label.txt
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_cpu_1/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_cpu_10/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_cpu_2/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_cpu_3/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_cpu_4/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_cpu_5/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_cpu_6/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_cpu_7/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_cpu_8/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_cpu_9/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_mem_1/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_mem_10/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_mem_2/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_mem_3/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_mem_4/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_mem_5/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_mem_6/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_mem_7/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_mem_8/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_mem_9/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_net_1/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_net_10/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_net_2/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_net_3/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_net_4/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_net_5/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_net_7/
│└── │├── │├── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_net_8/
│└── │├── │└── edge-2_pod_carts-edge-qsvjv_carts-edge-qsvjv-855dfb4465-lmdc6_net_9/
│└── │├── catalogue-cloud/
│└── │├── │├── catalogue-cloud_label.txt
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_cpu_1/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_cpu_10/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_cpu_2/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_cpu_3/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_cpu_4/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_cpu_5/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_cpu_6/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_cpu_7/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_cpu_8/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_cpu_9/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_mem_1/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_mem_10/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_mem_2/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_mem_3/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_mem_4/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_mem_5/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_mem_6/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_mem_7/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_mem_8/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_mem_9/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_net_1/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_net_10/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_net_2/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_net_3/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_net_4/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_net_5/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_net_6/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_net_7/
│└── │├── │├── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_net_8/
│└── │├── │└── cloud_pod_catalogue-cloud-mdwvc_catalogue-cloud-mdwvc-57bdfd65c7-qn5ks_net_9/
│└── │├── catalogue-edge/
│└── │├── │├── catalogue-edge_label.txt
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_cpu_1/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_cpu_10/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_cpu_2/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_cpu_3/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_cpu_4/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_cpu_5/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_cpu_6/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_cpu_7/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_cpu_8/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_cpu_9/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_mem_1/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_mem_10/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_mem_2/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_mem_3/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_mem_4/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_mem_5/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_mem_6/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_mem_7/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_mem_8/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_mem_9/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_net_1/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_net_10/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_net_2/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_net_3/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_net_4/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_net_5/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_net_6/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_net_7/
│└── │├── │├── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_net_8/
│└── │├── │└── edge-2_pod_catalogue-edge-ksjlr_catalogue-edge-ksjlr-d5f564966-pgzhf_net_9/
│└── │├── front-end-cloud/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_cpu_1/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_cpu_10/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_cpu_2/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_cpu_3/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_cpu_4/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_cpu_5/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_cpu_6/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_cpu_7/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_cpu_8/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_cpu_9/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_mem_1/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_mem_10/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_mem_2/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_mem_3/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_mem_4/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_mem_5/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_mem_6/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_mem_7/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_mem_8/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_mem_9/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_net_1/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_net_10/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_net_2/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_net_3/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_net_4/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_net_5/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_net_6/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_net_7/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_net_8/
│└── │├── │├── cloud_pod_front-end-cloud-6qdjr_front-end-cloud-6qdjr-79cd4bb769-9q8tf_net_9/
│└── │├── │└── front-end-cloud_label.txt
│└── │├── orders-cloud/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_cpu_1/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_cpu_10/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_cpu_2/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_cpu_3/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_cpu_4/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_cpu_5/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_cpu_6/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_cpu_7/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_cpu_8/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_cpu_9/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_mem_1/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_mem_10/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_mem_2/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_mem_3/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_mem_4/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_mem_5/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_mem_6/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_mem_7/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_mem_8/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_mem_9/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_net_1/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_net_10/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_net_2/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_net_3/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_net_4/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_net_5/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_net_6/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_net_7/
│└── │├── │├── cloud_pod_orders-cloud-bdjpf_orders-cloud-bdjpf-59d96f9dd7-7pxlx_net_9/
│└── │├── │└── orders-cloud_label.txt
│└── │├── orders-edge/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_cpu_1/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_cpu_10/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_cpu_2/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_cpu_3/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_cpu_4/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_cpu_5/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_cpu_6/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_cpu_7/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_cpu_8/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_cpu_9/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_mem_1/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_mem_10/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_mem_2/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_mem_3/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_mem_4/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_mem_5/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_mem_6/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_mem_7/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_mem_8/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_mem_9/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_net_1/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_net_10/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_net_2/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_net_3/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_net_4/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_net_5/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_net_6/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_net_7/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_net_8/
│└── │├── │├── edge-2_pod_orders-edge-g7m96_orders-edge-g7m96-656b549444-wgsb2_net_9/
│└── │├── │└── orders-edge_label.txt
│└── │├── payment-cloud/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_cpu_1/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_cpu_10/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_cpu_2/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_cpu_3/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_cpu_4/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_cpu_5/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_cpu_6/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_cpu_7/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_cpu_8/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_cpu_9/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_mem_1/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_mem_10/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_mem_2/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_mem_3/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_mem_4/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_mem_5/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_mem_6/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_mem_7/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_mem_8/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_mem_9/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_net_1/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_net_2/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_net_3/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_net_4/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_net_5/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_net_6/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_net_7/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_net_8/
│└── │├── │├── cloud_pod_payment-cloud-662lb_payment-cloud-662lb-7988cf58c-hmhwn_net_9/
│└── │├── │└── payment-cloud_label.txt
│└── │├── payment-edge/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_cpu_1/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_cpu_10/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_cpu_2/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_cpu_3/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_cpu_4/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_cpu_5/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_cpu_6/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_cpu_7/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_cpu_8/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_cpu_9/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_mem_1/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_mem_10/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_mem_2/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_mem_3/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_mem_4/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_mem_5/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_mem_6/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_mem_7/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_mem_8/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_mem_9/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_net_1/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_net_10/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_net_2/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_net_3/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_net_4/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_net_5/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_net_6/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_net_7/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_net_8/
│└── │├── │├── edge-2_payment-edge-5vmnc_payment-edge-5vmnc-84b4b88b88-swmpm_net_9/
│└── │├── │└── payment-edge_label.txt
│└── │├── shipping-cloud/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_cpu_1/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_cpu_10/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_cpu_2/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_cpu_3/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_cpu_4/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_cpu_5/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_cpu_6/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_cpu_7/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_cpu_8/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_cpu_9/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_mem_1/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_mem_10/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_mem_2/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_mem_3/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_mem_4/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_mem_5/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_mem_6/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_mem_7/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_mem_8/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_mem_9/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_net_1/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_net_10/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_net_2/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_net_3/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_net_4/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_net_5/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_net_6/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_net_7/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_net_8/
│└── │├── │├── cloud_pod_shipping-cloud-zzp2r_shipping-cloud-zzp2r-6df8b7fcc7-5gz8s_net_9/
│└── │├── │├── shipping-cloud_label.txt
│└── │├── shipping-edge/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_cpu_1/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_cpu_10/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_cpu_2/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_cpu_3/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_cpu_4/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_cpu_5/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_cpu_6/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_cpu_7/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_mem_1/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_mem_10/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_mem_2/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_mem_3/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_mem_4/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_mem_5/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_mem_6/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_mem_7/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_mem_8/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_mem_9/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_net_1/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_net_10/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_net_2/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_net_3/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_net_4/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_net_5/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_net_6/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_net_7/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_net_8/
│└── │├── │├── edge-2_pod_shipping-edge-nz2mm_shipping-edge-nz2mm-7599645b99-g56zq_net_9/
│└── │├── │├── shipping-edge_label.txt
│└── │├── user-cloud/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_cpu_1/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_cpu_10/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_cpu_2/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_cpu_3/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_cpu_4/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_cpu_5/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_cpu_6/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_cpu_7/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_cpu_8/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_cpu_9/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_mem_1/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_mem_10/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_mem_2/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_mem_3/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_mem_4/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_mem_5/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_mem_6/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_mem_7/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_mem_8/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_mem_9/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_net_1/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_net_10/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_net_2/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_net_3/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_net_4/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_net_5/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_net_6/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_net_7/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_net_8/
│└── │├── │├── cloud_pod_user-cloud-9x99q_user-cloud-9x99q-78558b8df5-b9gfk_net_9/
│└── │├── │└── user-cloud_label.txt
│└── │└── user-edge/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_cpu_1/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_cpu_10/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_cpu_2/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_cpu_3/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_cpu_4/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_cpu_5/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_cpu_6/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_cpu_7/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_cpu_8/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_cpu_9/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_mem_1/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_mem_10/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_mem_2/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_mem_3/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_mem_4/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_mem_5/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_mem_6/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_mem_7/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_mem_8/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_mem_9/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_net_1/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_net_10/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_net_2/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_net_3/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_net_4/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_net_5/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_net_6/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_net_7/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_net_8/
│└── │└── │├── edge-2_pod_user-edge-2rz4x_user-edge-2rz4x-597884bd65-vgmmm_net_9/
│└── │└── │└── user-edge_label.txt

```

## License

This project is licensed under the Apache 2.0 License - see the [LICENSE](LICENSE) file for details.

