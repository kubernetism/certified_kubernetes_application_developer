# Chapter 05: Pods and Namespaces - Solutions

## Practice Questions - Solutions

### Question 1: Pod Architecture
**Question:** What are the key components of a Kubernetes pod and how do they work together?
**Correct Answer:** A pod consists of:
- **Containers:** One or more application containers
- **Pod IP:** Shared network namespace for all containers in the pod
- **Volumes:** Shared storage accessible to all containers
- **Pod specification:** YAML/JSON configuration defining the pod

**How they work together:** All containers in a pod share the same network namespace (same IP address and port space), can communicate via localhost, and can share storage volumes through volume mounts.

### Question 2: Pod Lifecycle
**Question:** Describe the different phases of a pod's lifecycle and what triggers each phase.
**Correct Answer:**
- **Pending:** Pod is accepted but not yet scheduled to a node
- **Running:** Pod is bound to a node and at least one container is running
- **Succeeded:** All containers terminated successfully
- **Failed:** All containers terminated, at least one with failure
- **Unknown:** State cannot be determined (typically due to node communication issues)

**Triggers:** Pod phases are triggered by the kubelet, scheduler, and container runtime based on pod status, container states, and node communication.

### Question 3: Pod Specifications
**Question:** What are the essential fields in a pod specification and their purposes?
**Correct Answer:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-name
  namespace: namespace-name
spec:
  containers:
  - name: container-name
    image: image:tag
  restartPolicy: Always|Never|OnFailure
  nodeName: specific-node-name
  tolerations: ...
  affinity: ...
```

**Essential fields:**
- `apiVersion`: Kubernetes API version
- `kind`: Object type (Pod)
- `metadata.name`: Pod name
- `spec.containers`: Container specifications
- `spec.restartPolicy`: Restart behavior

### Question 4: Pod Networking
**Question:** How do pods communicate with each other in Kubernetes?
**Correct Answer:** Pods communicate through:
- **Cluster IP:** Services provide stable endpoints for pods
- **DNS:** Kubernetes DNS service resolves pod names
- **Host networks:** Pods can use host network namespace
- **Pod-to-pod:** Direct communication via pod IPs (in same namespace)
- **Cross-namespace:** Using fully qualified names (pod.namespace.svc.cluster.local)

### Question 5: Namespaces
**Question:** What are namespaces and how do they provide isolation in Kubernetes?
**Correct Answer:** Namespaces provide virtual sub-clusters within a physical cluster:
- **Resource isolation:** Separate object sets and resource quotas
- **Multi-tenancy:** Different teams/projects can share a cluster
- **Access control:** RBAC policies scoped to namespaces
- **Network isolation:** Services are namespace-scoped

**Common namespaces:**
- `default`: Default namespace
- `kube-system`: Kubernetes system components
- `kube-public`: Public resources
- Custom namespaces for applications

### Question 6: Pod Health Checks
**Question:** What are the different types of probes used to monitor pod health and how do they work?
**Correct Answer:**
- **Liveness Probe:** Determines if a container is running. If failed, the container is restarted.
- **Readiness Probe:** Determines if a container is ready to accept traffic. If failed, the container is removed from service endpoints.
- **Startup Probe:** Determines if a container has started. Used for containers with slow startup times.

**Probe types:**
- **HTTP GET:** Checks HTTP endpoint
- **TCP Socket:** Checks TCP port
- **Exec:** Runs command in container

### Question 7: Pod Scheduling
**Question:** What factors influence pod scheduling in Kubernetes?
**Correct Answer:** Scheduling is influenced by:
- **Resource requirements:** CPU/memory requests and limits
- **Node selection:** Node affinity/anti-affinity rules
- **Taints and tolerations:** Node restrictions and pod acceptance
- **Pod affinity:** Co-location or separation requirements
- **Resource availability:** Node capacity and allocatable resources
- **Topology constraints:** Zone, rack, and other topology requirements
- **Priority:** Higher priority pods get scheduled first

---

*Note: These solutions are based on Kubernetes documentation. Always verify with the latest official resources.*