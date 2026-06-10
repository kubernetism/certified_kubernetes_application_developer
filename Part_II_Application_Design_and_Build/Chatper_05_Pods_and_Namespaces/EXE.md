# Sample Exercises — Pods and Namespaces

> Solutions to these exercises are available in Appendix A.

---

### Exercise 1 — nginx Pod in a Namespace

1. Create a new Pod named `nginx` running the image `nginx:1.17.10`. Expose the container port `80`. The Pod should live in the namespace named `ckad`.

2. Get the details of the Pod including its IP address.

3. Create a temporary Pod that uses the `busybox:1.36.1` image to execute a `wget` command inside of the container. The `wget` command should access the endpoint exposed by the nginx container. You should see the HTML response body rendered in the terminal.

4. Get the logs of the nginx container.

5. Add the environment variables `DB_URL=postgresql://mydb:5432` and `DB_USERNAME=admin` to the container of the nginx Pod.

6. Open a shell for the nginx container and inspect the contents of the current directory `ls -l`. Exit out of the container.

<details>
<summary>Solution</summary>

```bash
# Step 1: Create the namespace and Pod
$ kubectl create namespace ckad
$ kubectl run nginx --image=nginx:1.17.10 --port=80 --namespace=ckad
```

Or using a YAML manifest:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: ckad
spec:
  containers:
  - name: nginx
    image: nginx:1.17.10
    ports:
    - containerPort: 80
```

```bash
$ kubectl apply -f nginx-pod.yaml
```

```bash
# Step 2: Get Pod details including IP address
$ kubectl get pod nginx --namespace=ckad -o wide
# or for full details
$ kubectl describe pod nginx --namespace=ckad
```

```bash
# Step 3: Create a temporary busybox Pod to wget the nginx endpoint
# First, get the nginx Pod IP
$ kubectl get pod nginx --namespace=ckad -o wide

# Run the temporary Pod (replace <nginx-pod-ip> with actual IP)
$ kubectl run busybox --image=busybox:1.36.1 --rm -it --restart=Never \
  --namespace=ckad -- wget -O- <nginx-pod-ip>:80
```

```bash
# Step 4: Get nginx container logs
$ kubectl logs nginx --namespace=ckad
```

```bash
# Step 5: Add environment variables to the nginx Pod
# Edit the Pod manifest and add env section:
$ kubectl edit pod nginx --namespace=ckad
```

Updated container spec:

```yaml
containers:
- name: nginx
  image: nginx:1.17.10
  ports:
  - containerPort: 80
  env:
  - name: DB_URL
    value: "postgresql://mydb:5432"
  - name: DB_USERNAME
    value: "admin"
```

> **Note:** Since Pods are largely immutable, you may need to delete and recreate the Pod with the updated manifest.

```bash
# Step 6: Open a shell into the nginx container
$ kubectl exec -it nginx --namespace=ckad -- /bin/sh

# Inside the container
$ ls -l

# Exit the container
$ exit
```

</details>

---

### Exercise 2 — Loop Pod with busybox

1. Create a YAML manifest for a Pod named `loop` that runs the `busybox:1.36.1` image in a container. The container should run the following command:
   ```
   for i in {1..10}; do echo "Welcome $i times"; done
   ```
   Create the Pod from the YAML manifest. What's the status of the Pod?

2. Edit the Pod named `loop`. Change the command to run in an endless loop. Each iteration should echo the current date.

3. Inspect the events and the status of the Pod `loop`.

<details>
<summary>Solution</summary>

```yaml
# loop-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: loop
spec:
  containers:
  - name: loop
    image: busybox:1.36.1
    command: ["/bin/sh", "-c"]
    args:
    - "for i in {1..10}; do echo \"Welcome $i times\"; done"
```

```bash
# Create the Pod
$ kubectl apply -f loop-pod.yaml

# Check the status
$ kubectl get pod loop
```

> **Expected status:** The Pod will show `Completed` status after the loop finishes its 10 iterations, since the container process exits normally.

---

```bash
# Step 2: Edit the Pod to run an endless loop
$ kubectl edit pod loop
```

Updated command in the manifest:

```yaml
containers:
- name: loop
  image: busybox:1.36.1
  command: ["/bin/sh", "-c"]
  args:
  - "while true; do echo $(date); sleep 1; done"
```

> **Note:** Because Pods are immutable, `kubectl edit` may not apply the command change directly. Delete and recreate the Pod with the updated manifest:

```bash
$ kubectl delete pod loop
$ kubectl apply -f loop-pod.yaml
```

---

```bash
# Step 3: Inspect events and status of the loop Pod
$ kubectl describe pod loop

# Check current status
$ kubectl get pod loop

# View live logs to confirm the date is echoing
$ kubectl logs -f loop
```

> **Expected status:** The Pod will remain in `Running` state indefinitely since the endless loop keeps the container process alive. The `kubectl describe` output will show the container state as `Running` and list any relevant events.

</details>