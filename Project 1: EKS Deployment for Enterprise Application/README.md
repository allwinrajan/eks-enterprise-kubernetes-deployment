## Introduction

1. What is EKS
2. Why is EKS
3. When we need to go with EKS
4. What is MasterNode/ControlPlane
5. What is WorkerNode/DataPlane
6. Why HA Kubernetes Architecture need Three Masternode and Workernode while Single Masternode and Workernode
7. What is self managed Kubernetes ? How to Setup in AWS ?
8. Master Node -> API Server, ETCD, Scheduler, Controller Manager, Cloud Control Manager ?
9. Worker Node -> CNI (Container Network Interface), CRI (Container Runtime Interface), Kube Proxy, Kubelet, DNS, Join this into Control plane ?
10. Why done this confige by manual cause ERROR PRONE ?
11. How reduce effort by Kops rather than Kubeadm ? Diffrence bt Kubeadm and Kops?
12. Manual POV Problems: Master node went down ?, Certificate expired / Renew, API server down / Slow, ETCD crossed, Scheduler is not working ? why this happen even in KOPS ?
13. Its for only one cluster what happen when ORG have 100 clusters or 1000 clusters its headache for DevOps Engineer ?
14. How to manage it as Cloud/DevOps Engineer POV ?
15. EKS is managed Control plane ?
16. When we request a EKS service it give Fully Managed Kubernetes Cluster by AWS with respective control plane ? Taken care by AWS ? HA ?
17. How we attached Dataplane / Workernode to the created EKS's Control plane ?
18. What are the ways to create worker node by manual in AWS that allows we to run a container ?
19. How we go with Ec2 and Install all Worker Node confige ? What is the Pros and Cons ?
20. How we go with Fargate that is one of AWS Serverless Compute service like Lambda where it special for run a container unlike Lambda handle small workloads ?
21. Predict the Accuracy of these two combination ? EKS Control plane with Ec2 vs EKS Control plane with Fargate ?
22. Which one Robust and Highly stable Kubernetes Cluster ?
23. If we go with Ec2 How much we Architect the highly available Dataplane / Worker node ? threshold, monitoring, autoscaling, Multi AZ ?
24. EKS is the fully managed Control plane of AWS for Kubernetes and using this How EKS significantly reduce the configuration ? and How it manages all the issues as we mentioned ?
25. If issue arrised by EKS how to handle by AWS SLA ? What is compansation for issue that happening in EKS control plane ?
26. Why people are moving to EKS ?
27. If we are in AWS What is the Two way of Installing Kubernetes ? i) Using Ec2 (VM) and continue with Kops / Kubeadm / Minikube ? ii) Go with EKS ?
28. Drawbacks of EKS ?
29. How to install, configure and manage the kubernetes on on-premises ?
## Todays Agenda

### Types of Services in Kubernetes and Their Use Cases

| **Service Type**     | **Accessibility**                  | **Description**                                                                                  | **Real-Time Example**                                               |
| -------------------- | ---------------------------------- | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| **ClusterIP**        | Internal (within the cluster)      | Assigns an internal IP, accessible only inside the cluster for service-to-service communication. | Microservices in the same cluster talk to each other.               |
| **NodePort**         | External via `<NodeIP>:<NodePort>` | Opens a static port (30000–32767) on all nodes for external access.                              | Accessing a web app by hitting `http://<NodeIP>:30080`.             |
| **LoadBalancer**     | External (Internet)                | Creates an external load balancer (cloud provider) and assigns a public IP.                      | Hosting a production app on AWS/GCP with public access.             |
| **ExternalName**     | External DNS mapping               | Maps service to an external DNS name; no proxying.                                               | Connecting to an external database `db.example.com`.                |
| **Headless Service** | Internal, direct pod DNS           | No ClusterIP; gives direct DNS entries for pods, used for stateful apps.                         | Cassandra or MySQL cluster where each pod is accessed individually. |

**1. ClusterIP (Default)**
- It is the default Service type in Kubernetes.
- Provides an internal virtual IP accessible only within the cluster.
- Pods use this IP to communicate with other services internally.
- It does not allow external traffic from outside the cluster.
- Ideal for microservice-to-microservice communication.

Example: Frontend service calling a backend service inside the cluster.

**2. NodePort**
- Exposes the service on a static port (30000–32767) on every Node.
- External users can access it using <NodeIP>:<NodePort>.
- Useful when you need basic external access without a load balancer.
- The NodePort forwards requests to the corresponding ClusterIP Service.
- Works in any environment, even without a cloud provider.

Example: Accessing a web app at http://192.168.1.10:30080.

**3. LoadBalancer**
- Integrates with cloud providers (AWS, GCP, Azure) to create an external Load Balancer.
- Assigns a public IP for external users to access the service.
- Distributes traffic automatically across multiple pods.
- Best for production environments where public access is required.
- Requires a supported cloud environment or MetalLB in bare metal setups.

Example: A customer-facing e-commerce website running on Kubernetes.

**4. ExternalName**
- Maps a Kubernetes Service to an external DNS name instead of IP.
- Does not create a proxy or open ports inside the cluster.
- It simply returns a CNAME record pointing to the external service.
- Useful for connecting cluster apps to external APIs or databases.
- Reduces the need to hardcode external endpoints in application code.

Example: Connecting to db.example.com for an external database.

**5. Headless Service**
- Created by setting ClusterIP: None in the Service definition.
- Does not assign a virtual IP; instead, provides direct DNS records for pods.
- Enables clients to connect directly to individual pods.
- Commonly used for stateful apps or databases that need identity.
- Works with StatefulSets for stable network identities.

Example: Cassandra or MySQL cluster for direct pod access.


