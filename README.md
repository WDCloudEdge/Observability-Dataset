# Observability

## Description

Observability datasets of hybrid-deployed microservice systems in the cloud-edge collaborative environment.


## Dataset

### Download

[Dropbox](https://www.dropbox.com/scl/fi/s6gugabhlfd4ar46vu3nf/abnormal.zip?rlkey=iztl9kqkorakqt6dxocmlv3k7&st=jsbbcozk&dl=0)

### Description

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
| call.csv         | Time-series call latency between microservices is denoted by P99, P95, and P90, which denote the 99th, 95th, and 90th percentiles of the latency data.                                                                  |
| graph.csv        | Time-series topologies denote the instance, the server where it is located, and the service call link.                                                                                                                  |
| instance.csv     | Time-series metrics of each instance, containing CPU usage, memory usage, and network transmit packets.                                                                                                                 |
| latency.csv      | The time-series latency of microservices is denoted by P99, P95, and P90, which denote the 99th, 95th, and 90th percentiles of the latency data.                                                                        |
| resource.csv     | Time-series metrics of instances within a specific namespace, containing the total CPU usage and memory usage                                                                                                           |
| success_rate.csv | Time-series success rate of microservices                                                                                                                                                                               |
| svc_metric.csv   | Time-series metrics of microservices (the average of its instances), containing CPU usage, CPU limit, memory usage, memory limit, FS write, FS read, FS usage, net receive, net transmit, and network transmit packets. |
| svc_qps.csv      | Time-series query per second of microservices                                                                                                                                                                           |

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

## Project Structure

```textile

```
