# Chapter 02: Kubernetes in a Nutshell - Solutions

## Practice Questions - Solutions

### Question 1: Architecture Components
**Question:** What are the main components of Kubernetes architecture and their roles?
**Correct Answer:**
- **Control Plane:**
  - API Server: Exposes Kubernetes API and handles requests
  - etcd: Distributed key-value store for cluster state
  - Scheduler: Assigns pods to nodes
  - Controller Manager: Runs controller processes
- **Worker Nodes:**
  - Kubelet: Agent that manages pods on nodes
  - Kube-proxy: Maintains network rules
  - Container Runtime: Runs containers (Docker, containerd, etc.)

### Question 2: Pods and Containers
**Question:** Explain the relationship between pods and containers in Kubernetes.
**Correct Answer:** A pod is the smallest deployable unit in Kubernetes, containing one or more containers that share:
- Network namespace (share IP address and port space)
- Storage volumes
- Container runtime settings
Pods are ephemeral and can contain multiple containers that work together as a cohesive unit.

### Question 3: Kubernetes Services
**Question:** What are the different types of Kubernetes Services and when would you use each?
**Correct Answer:**
- **ClusterIP:** Internal service, only accessible within the cluster (default)
- **NodePort:** Exposes service on each node's IP at a static port
- **LoadBalancer:** Exposes service externally using cloud provider's load balancer
- **ExternalName:** Maps service to external DNS name
- **Headless:** No cluster IP, DNS returns individual pod IPs

### Question 4: Namespaces
**Question:** Why are namespaces important in Kubernetes and how do they work?
**Correct Answer:** Namespaces provide scope for Kubernetes objects, enabling:
- Resource isolation between teams/projects
- Multi-tenancy in shared clusters
- Quota management and resource allocation
- Access control separation
They work by providing virtual sub-clusters within a physical cluster, with each namespace having its own set of objects and resource limits.

### Question 5: Kubernetes Objects
**Question:** List and describe five different types of Kubernetes objects.
**Correct Answer:**
- **Pod:** Smallest deployable unit, contains one or more containers
- **Deployment:** Manages pod replicas and updates
- **Service:** Provides network access to pods
- **ConfigMap:** Stores configuration data
- **Secret:** Stores sensitive configuration data
- **PersistentVolumeClaim:** Requests storage resources
- **Ingress:** Manages external access to services

### Question 6: kubectl Commands
**Question:** What is the difference between `kubectl get` and `kubectl describe` commands?
**Correct Answer:**
- **`kubectl get`:** Lists Kubernetes objects with basic information (name, status, etc.)
- **`kubectl describe`:** Provides detailed information about a specific object, including events, status conditions, and configuration details

---

*Note: These solutions are based on Kubernetes documentation. Always verify with the latest official resources.*