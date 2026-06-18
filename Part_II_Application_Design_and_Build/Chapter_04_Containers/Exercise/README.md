# Chapter 4: Containers — Questions (Sample Exercises)

> Solutions to these exercises are available in Appendix A of the book.

**1.** Navigate to the directory `app-a/ch04/containerized-java-app` of the checked-out GitHub repository `bmuschko/ckad-study-guide`. Inspect the Dockerfile.
- Build the container image from the Dockerfile with the tag `nodejs-hello-world:1.0.0`.
- Run a container with the container image. Make the application available on port 80.
- Execute a `curl` or `wget` command against the application's endpoint.
- Retrieve the container logs.

**2.** Modify the Dockerfile from the previous exercise. Change the base image to the tag `20.4-alpine` and the working directory to `/node`.
- Build the container image from the Dockerfile with the tag `nodejs-hello-world:1.1.0`.
- Ensure that the container image has been created by listing it.

**3.** Pull the container image `alpine:3.18.2` available on Docker Hub.
- Save the container image to the file `alpine-3.18.2.tar`.
- Delete the container image. Verify the container image is not listable anymore.
- Reinstate the container image from the file `alpine-3.18.2.tar`.
- Verify that the container image can be listed.

---
**Book:** CKAD Study Guide
**Author:** Benjamin Muschko
**Chapter:** 4 — Containers (pp. 33–41)