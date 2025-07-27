Introduction

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
### Todays Agenda

1. Let's say we have three master node (m1, m2, m3) and two worker node (w1, w2), we deployed an application on w2, so typically the task is how we are going to allow th exteral users
   to access my application that deployed in kubernetes cluster

2. For that we need to run a pod through services by kubectl and service give three options 1 is we can use ClusterIP (Only Accesible within the cluster components like master node (m1, m2, m3)
   worker node (w1,w2))
   that we already have 2 is Using Nodeport that is Node level 3 is using
   load balancer
   
