## Orchestration Advantages
#### Kubernetes-based Service

TKE is developed on the basis of Kubernetes (K8s), a container cluster management system made open-source by Google. Leveraging the Docker technology, Kubernetes provides containerized applications with a complete set of features ranging from deployment and execution and resource scheduling to service discovery and dynamic scaling, making it much easier to manage large-scale container clusters.

### Benefits of Kubernetes

- Using elegant software engineering consisting of modularization and microservices, Kubernetes implements a modular design that allows you to customize network, storage, scheduling, monitoring, and log modules as needed through flexible plugins.
- The Kubernetes project community acts as an open-source platform for the implementation of container, network, and storage.

### TKE vs. Customer Self-built Container Service

| Advantage | Tencent Cloud TKE | Customer Self-built Container Service |
|---------|---------|---------|
| Ease of use | <b>Simplified cluster management </b><br> <li>TKE has various features such as large-scale container cluster management, resource scheduling, container arrangement, and code construction. It blocks the differences of underlying infrastructures and simplifies management and OPS of distributed applications. You no longer need to use cluster management software or design fault-tolerating cluster structures, thus eliminating all relevant management and scaling workloads. <li>You just need to enable a container cluster and specify the tasks you want to run, and TKE will help you complete all the cluster management work, enabling you to focus on developing Dockerized applications. | When using a self-built container management infrastructure, you usually need to go through complex management processes such as installing, operating, and scaling your own cluster management software as well as configuring management systems and monitoring solutions. |
| Flexible scalability | <b>Flexible cluster management and integration with CLB </b><br> <li>You can use TKE to schedule long-running applications and batch jobs flexibly. You can also use APIs to obtain the latest cluster status for easy integration with your customized and third-party scheduling applications. <li>TKE is integrated with CLB, enabling you to distribute traffic among multiple containers. You just need to specify the container configuration and load balancer to be used, and the TKE management application will automatically add/delete resources for you. In addition, TKE can auto-recover faulty containers to guarantee that a sufficient number of containers is always running to sustain your applications. | You need to determine how to manually deploy container services according to the business traffic and health status, which has poor availability and scalability. |
| Security and stability | <b>High isolation of resources and high availability of services </b><br><li>TKE works inside your own CVM instance without sharing computing resources with other customers. <li>Your clusters run inside VPCs where you can use your own security groups and network ACLs. These features enable a high level of isolation and help you use CVM instances to construct applications with high security and reliability. <li>TKE uses a distributed service structure to implement auto failover and fast migration for services while ensuring high security and availability of services and data together with distributed backend storage of stateful services. | Due to kernel issues and imperfect namespaces of self-built container services, isolation at the tenant, device, and kernel module levels is rather poor. |
| High efficiency | <b>Fast image deployment and continuous business integration </b><br><li>TKE runs inside your VPCs where quality BGP networks ensure fast upload and download of images and make high numbers of containers able to launch within seconds, greatly reducing operational overheads and enabling you to focus more on business operations. <li>You can deploy your businesses on TKE. After code is submitted to GitHub or other code hosting platforms, TKE can immediately create, test, pack, and integrate services and deploy the integrated code in pre-release and production environments. | The efficiency of using images to create containers cannot be guaranteed as the network quality of self-built container services may fluctuate significantly. |
| Low cost | <b>Free of charge TKE services </b><br>There are no extra fees for using TKE, and APIs can be called in containers for free to create cluster management applications. You only need to pay for the Tencent Cloud service resources created for storage and running applications, such as CVM and CBS. | You need to spend big money creating, installing, operating, maintaining, and scaling your own cluster management infrastructures. |

### TKE Monitoring vs. Self-built Container Monitoring
TKE monitoring collects and displays comprehensive statistics of around 30 metrics such as cluster, service, pod, and container, allowing you to check cluster health and create alarms accordingly. In addition, more metrics will be available soon.

| Advantage | TKE | Self-built Container Service |
|---------|---------|---------|
| Complete set of metrics | Approximately 30 metrics are available, including cluster, service, container, and pod. | Only a few metrics are available and in-house development is required. |
| Low construction cost | TKE monitoring is provided when a cluster is created. | Monitoring needs to be constructed manually and and is very expensive. |
| Low OPS cost | Metric OPS is performed by the platform with guaranteed data accuracy. | Metrics need to be maintained manually. |
| Low storage cost | The data of each metric in the past three months is retained free of charge. | Fees are charged based on the storage size. |
| High scalability | TKE continues to improve and add new metrics. | Developers are required to construct new metrics. |
| Alarming | Available | Unavailable |
| Troubleshooting | Container logs can be viewed in the console and WebShell can be used to quickly log in to containers for troubleshooting. | You need to manually log in to containers or servers for troubleshooting. |
