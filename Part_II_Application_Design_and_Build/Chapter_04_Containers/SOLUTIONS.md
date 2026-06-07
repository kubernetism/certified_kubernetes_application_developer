# Chapter 04: Containers - Solutions

## Practice Questions - Solutions

### Question 1: Container Fundamentals
**Question:** What is a container and how does it differ from a virtual machine?
**Correct Answer:** A container is a lightweight, standalone package that includes an application and its dependencies, sharing the host OS kernel. Unlike VMs, containers don't need a separate OS kernel and use fewer resources.

**Key Differences:**
- **Containers:** Share host kernel, start in seconds, smaller size, higher density
- **VMs:** Have separate OS, take minutes to start, larger size, lower density

### Question 2: Docker Best Practices
**Question:** What are the key best practices for creating efficient Docker images?
**Correct Answer:**
- Use specific base images (e.g., `python:3.9-slim` instead of `python:latest`)
- Minimize layers by combining commands
- Use `.dockerignore` to exclude unnecessary files
- Run applications as non-root users
- Use multi-stage builds
- Keep images small and focused on single purposes
- Use specific version tags instead of `latest`
- Implement proper cleanup in Dockerfiles

### Question 3: Image Optimization
**Question:** How can you optimize Docker images for size and security?
**Correct Answer:**
- **Size Optimization:**
  - Use smaller base images (`alpine`, `slim`)
  - Implement multi-stage builds
  - Clean up package caches
  - Use `.dockerignore` effectively
  - Use specific version tags

- **Security Optimization:**
  - Run containers as non-root users
  - Use minimal base images
  - Regularly update base images
  - Scan images for vulnerabilities
  - Use read-only root filesystems
  - Implement proper resource limits

### Question 4: Multi-stage Builds
**Question:** Explain the concept of multi-stage builds and provide an example.
**Correct Answer:** Multi-stage builds use multiple `FROM` statements in a Dockerfile to create smaller, more secure final images by separating build dependencies from runtime dependencies.

**Example:**
```dockerfile
# Build stage
FROM golang:1.19 as builder
WORKDIR /app
COPY . .
RUN go build -o myapp

# Runtime stage
FROM alpine:3.18
WORKDIR /app
COPY --from=builder /app/myapp .
CMD ["./myapp"]
```

### Question 5: Container Security
**Question:** What are important security considerations when running containers in Kubernetes?
**Correct Answer:**
- **Security Context:** Run containers as non-root users
- **Image Scanning:** Scan images for vulnerabilities
- **Network Security:** Use network policies and secrets management
- **Resource Limits:** Set appropriate CPU/memory limits
- **RBAC:** Implement proper role-based access control
- **Pod Security Policies:** Enforce security constraints
- **Secrets Management:** Use Kubernetes secrets or external secret managers
- **Runtime Security:** Use runtime security tools

### Question 6: Resource Management
**Question:** How do you set resource limits and requests for containers in Kubernetes?
**Correct Answer:** Resource limits and requests are set in the container spec:

```yaml
resources:
  requests:
    memory: "64Mi"
    cpu: "250m"
  limits:
    memory: "128Mi"
    cpu: "500m"
```

- **Requests:** Minimum resources guaranteed to the container
- **Limits:** Maximum resources the container can use
- CPU is measured in millicores (1 CPU = 1000m)
- Memory is measured in bytes (Mi = mebibytes, Gi = gibibytes)

---

*Note: These solutions are based on Docker and Kubernetes documentation. Always verify with the latest official resources.*