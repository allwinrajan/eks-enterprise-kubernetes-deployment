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

1. ClusterIP (Default) 
ClusterIP is the default Service type in Kubernetes. It gives an internal IP that works only inside the cluster, so apps can talk to each other privately. You cannot access it from outside the cluster. This is useful for backend services like a database or an internal API that should not be exposed to the internet.

2. NodePort
NodePort makes the Service accessible from outside the cluster by opening a fixed port (range 30000–32767) on all nodes. You can access the app using NodeIP:NodePort from your browser or a client. It is built on top of ClusterIP. Good for basic external access, but not the best for production because it’s hard to manage and less secure.

3. LoadBalancer
LoadBalancer is used to make your app accessible from the internet in a simple way. It asks your cloud provider (like AWS, GCP, or Azure) to create a load balancer and gives you a public IP. It automatically sends traffic to the right pods and balances the load. This is the best choice for production apps that users access online.

4. ExternalName
ExternalName does not create a real Service like others. Instead, it maps your service to an external DNS name (like api.example.com). It does not open any ports or route traffic inside Kubernetes. Useful when your app inside Kubernetes needs to talk to an external database or external API without hardcoding URLs.

5. Headless Service
Headless Service is made by setting ClusterIP: None. It does not give a single IP; instead, it gives DNS names for each pod. This is useful when apps need to connect to individual pods directly, like in databases or StatefulSets. Example: Cassandra cluster, where each node has its own identity.


 

