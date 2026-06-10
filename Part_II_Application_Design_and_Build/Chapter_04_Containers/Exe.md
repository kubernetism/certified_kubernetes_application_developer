# Sample Exercises

> Solutions to these exercises are available in Appendix A.

---

### Exercise 1 — Containerized Java App

1. Navigate to the directory `app-a/ch04/containerized-java-app` of the checked-out GitHub repository `bmuschko/ckad-study-guide`. Inspect the Dockerfile.
2. Build the container image from the Dockerfile with the tag `nodejs-hello-world:1.0.0`.
3. Run a container with the container image. Make the application available on port `80`.
4. Execute a `curl` or `wget` command against the application's endpoint.
5. Retrieve the container logs.

<details>
<summary>Solution</summary>

```bash
# Step 1: Navigate and inspect
$ cd app-a/ch04/containerized-java-app
$ cat Dockerfile

# Step 2: Build the image
$ docker build -t nodejs-hello-world:1.0.0 .

# Step 3: Run the container on port 80
$ docker run -d -p 80:3000 nodejs-hello-world:1.0.0

# Step 4: Test the endpoint
$ curl http://localhost:80
# or
$ wget -qO- http://localhost:80

# Step 5: Retrieve container logs
$ docker logs <container-id>
```

> **Tip:** Use `docker ps` to find the container ID after running it.

</details>

---

### Exercise 2 — Modify the Dockerfile

1. Modify the Dockerfile from the previous exercise. Change the base image to the tag `20.4-alpine` and the working directory to `/node`.
2. Build the container image from the Dockerfile with the tag `nodejs-hello-world:1.1.0`.
3. Ensure that the container image has been created by listing it.

<details>
<summary>Solution</summary>

```dockerfile
# Modified Dockerfile (relevant changes)
FROM node:20.4-alpine
WORKDIR /node
# ... rest of Dockerfile remains the same
```

```bash
# Step 2: Build the updated image
$ docker build -t nodejs-hello-world:1.1.0 .

# Step 3: List images to verify
$ docker images | grep nodejs-hello-world
```

Expected output:
```
nodejs-hello-world   1.1.0   <image-id>   ...
nodejs-hello-world   1.0.0   <image-id>   ...
```

</details>

---

### Exercise 3 — Pull, Save, Delete, and Restore an Image

1. Pull the container image `alpine:3.18.2` available on Docker Hub.
2. Save the container image to the file `alpine-3.18.2.tar`.
3. Delete the container image. Verify the container image is not listable anymore.
4. Reinstate the container image from the file `alpine-3.18.2.tar`.
5. Verify that the container image can be listed.

<details>
<summary>Solution</summary>

```bash
# Step 1: Pull the image
$ docker pull alpine:3.18.2

# Step 2: Save the image to a tar file
$ docker save alpine:3.18.2 -o alpine-3.18.2.tar

# Step 3: Delete the image and verify
$ docker rmi alpine:3.18.2
$ docker images | grep alpine
# Expected: no output (image is gone)

# Step 4: Restore the image from the tar file
$ docker load -i alpine-3.18.2.tar

# Step 5: Verify the image is listed again
$ docker images | grep alpine
# Expected output:
# alpine   3.18.2   <image-id>   ...
```

</details>