# Chapter 4: Containers — Summary

## Container Terminology
A container packages an application together with its runtime environment and configuration into a single unit, solving the "but it works on my machine" problem. Key terms:

- **Container runtime engine** — software that runs containers on a host OS (e.g., Docker Engine, containerd).
- **Container orchestrator** — uses a container runtime to instantiate containers while adding scalability and networking (Kubernetes is the prime example).
- **Containerization** — the process of bundling an app into a container, driven by instructions in a **Dockerfile**.
- **Container image** — the artifact produced by building a Dockerfile; published to a **container registry** (Docker Hub, GCR, Quay) for others to consume.
- **Container** — a running instance of an image.

In short: *Dockerfile = blueprint, image = artifact, container = running instance.*

## Containerizing a Java-Based Application
The chapter walks through containerizing a Spring Boot Java app end to end:

1. **Writing a Dockerfile** — defines the base image (`FROM`), working directory (`WORKDIR`), copies the compiled JAR (`COPY`), sets the startup command (`ENTRYPOINT`), and exposes a port (`EXPOSE`).
2. **Building the image** — `docker build -t <name>:<tag> .`, where `.` is the build context directory containing the Dockerfile and source files.
3. **Listing images** — `docker images` shows locally cached images.
4. **Running the container** — `docker run -d -p <host-port>:<container-port> <image>` runs it detached, with port forwarding.
5. **Listing containers** — `docker container ls` (add `-a` to include stopped containers).
6. **Interacting with the container** — `docker logs <id>` for troubleshooting output; `docker exec -it <id> bash` to get an interactive shell inside a running container.
7. **Publishing the image** — tag it with a registry-appropriate prefix using `docker tag`, authenticate with `docker login`, then `docker push` to share it via a registry like Docker Hub.
8. **Saving and loading images** — `docker save -o <file>.tar <image>` archives an image (including all layers/tags) to a file; `docker load --input <file>.tar` restores it without needing a registry.

## Exam Essentials
- Gain hands-on practice with the full containerization workflow: define, build, run, and publish an image, independent of Kubernetes itself.
- Be comfortable with Docker Engine specifically, since it remains the most widely used container runtime, but also be aware that alternatives like containerd and Podman exist.
- As an application developer, expect to define, build, and modify container images regularly — broader familiarity with the runtime engine's docs pays off.

## Key Takeaway
Before Kubernetes can run your application in a Pod, it must already exist as a container image. This chapter is entirely about the developer workflow *outside* Kubernetes — using Docker (or an equivalent runtime) to build, run, inspect, publish, and persist that image so it's ready to be deployed in later chapters.

---
**Book:** CKAD Study Guide
**Author:** Benjamin Muschko
**Chapter:** 4 — Containers (pp. 33–41)