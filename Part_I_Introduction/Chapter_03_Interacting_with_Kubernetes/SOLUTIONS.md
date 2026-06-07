# Chapter 03: Interacting with Kubernetes - Solutions

## Practice Questions - Solutions

### Question 1: kubectl Basics
**Question:** What are the most common kubectl commands and their purposes?
**Correct Answer:**
- **`kubectl get`:** Lists objects and their basic information
- **`kubectl create`:** Creates new objects from files or command line
- **`kubectl apply`:** Creates or updates objects declaratively
- **`kubectl delete`:** Deletes objects
- **`kubectl describe`:** Shows detailed information about objects
- **`kubectl logs`:** Shows container logs
- **`kubectl exec`:** Executes commands in containers
- **`kubectl scale`:** Scales deployments and replicasets
- **`kubectl rollout`:** Manages deployment rollouts

### Question 2: YAML Manifests
**Question:** What is the structure of a Kubernetes YAML manifest and what are the required fields?
**Correct Answer:** A Kubernetes YAML manifest has this structure:
```yaml
apiVersion: group/version
kind: ObjectKind
metadata:
  name: object-name
  namespace: namespace-name
spec:
  # object specification
```
Required fields:
- `apiVersion`: API version
- `kind`: Type of object (Pod, Deployment, Service, etc.)
- `metadata`: Object metadata including name

### Question 3: Context Management
**Question:** How do you switch between different Kubernetes contexts and what is the purpose of contexts?
**Correct Answer:**
- Switch contexts: `kubectl config use-context context-name`
- List contexts: `kubectl config get-contexts`
- Current context: `kubectl config current-context`
Purpose: Contexts store cluster, user, and namespace information, allowing easy switching between different Kubernetes clusters and configurations.

### Question 4: Namespace Operations
**Question:** What kubectl commands are used to manage namespaces and switch between them?
**Correct Answer:**
- Create namespace: `kubectl create namespace namespace-name`
- List namespaces: `kubectl get namespaces`
- Switch namespace: `kubectl config set-context --current --namespace=namespace-name`
- Use namespace: `kubectl get pods -n namespace-name`
- Delete namespace: `kubectl delete namespace namespace-name`

### Question 5: kubectl Plugins
**Question:** What are kubectl plugins and how do you create/use them?
**Correct Answer:** kubectl plugins are executable files that extend kubectl functionality:
- Naming convention: `kubectl-<command>`
- Location: Must be in PATH or $KREW_PLUGINS_PATH
- Use: Same as regular kubectl commands
- Example: `kubectl-view-allocations` (shows resource usage)

### Question 6: Output Formats
**Question:** What are the different output formats available in kubectl and when would you use each?
**Correct Answer:**
- **`-o yaml`:** YAML format, for creating manifests
- **`-o json`:** JSON format, for programmatic processing
- **`-o name`:** Resource names only, for scripting
- **`-o wide`:** Extended information, for detailed views
- **`-o jsonpath={.items[*].metadata.name}`:** Custom formatting with JSONPath
- **`-o go-template`:** Go template formatting for custom output

---

*Note: These solutions are based on Kubernetes documentation. Always verify with the latest official resources.*