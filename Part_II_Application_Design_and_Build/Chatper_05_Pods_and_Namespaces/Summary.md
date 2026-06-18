# Chapter 5: Pods and Namespaces — Summary

## The Pod
The Pod is the most important primitive in the Kubernetes API — it lets you run a containerized application. While most Pods run a single container, a Pod can wrap more than one (covered in Chapter 8) and can also consume other services like storage and configuration data.

## Working with Pods

**Creating Pods** — imperatively with `kubectl run` (e.g. `--image`, `--port`, `--env`, `--labels`), or declaratively from a YAML manifest using `kubectl apply -f`. The scheduler assigns the Pod to a node, and the container runtime pulls the image (from Docker Hub by default) if it isn't already cached there.

**Listing Pods** — `kubectl get pods` (or `get pods <name>` to query a specific one).

**Pod Life Cycle Phases** — `Pending` (accepted but image not yet pulled), `Running` (at least one container active), `Succeeded` (all containers exited cleanly), `Failed` (at least one container errored), `Unknown` (state can't be determined). These are distinct from container states (`Waiting`, `Running`, `Terminated`).

**Rendering Pod Details** — `kubectl describe pods <name>` shows metadata, containers, and the event log; can be piped through `grep` for specific fields.

**Accessing Logs** — `kubectl logs <name>` downloads container output; `-f` streams it live; `-p` retrieves logs from the *previous* container instance after a restart.

**Executing Commands** — `kubectl exec -it <name> -- /bin/sh` opens an interactive shell; dropping `-it` runs a single one-off command instead (e.g. `kubectl exec hazelcast -- env`).

**Temporary Pods** — `kubectl run ... --rm -it --restart=Never -- <command>` automatically deletes the Pod once the command finishes, useful for quick troubleshooting (e.g. curling another Pod's IP).

**Pod IP Addresses** — every Pod gets an IP on creation, visible via `-o wide` or `describe`. This IP is *not stable*: a restart leases a new one, so it's called a virtual IP. Stable inter-Pod communication instead relies on a Service (Chapter 21).

**Configuring Pods** — environment variables (`spec.containers[].env`) inject runtime configuration without needing per-environment images (a Twelve-Factor App principle). The `command` attribute overrides an image's `ENTRYPOINT`; `args` overrides `CMD`.

**Deleting Pods** — `kubectl delete pod <name>` (or `delete -f <file>.yaml`) performs a graceful deletion (5–30 second grace period by default); add `--now` to force immediate termination and save time (not recommended in production).

## Working with Namespaces
Namespaces scope object names to avoid naming collisions — useful for isolating objects by team or responsibility. A fresh cluster ships with `default`, `kube-node-lease`, `kube-public`, and `kube-system` (the `kube-` prefixed ones are system-managed).

- **Create:** `kubectl create namespace <name>`
- **Use:** `--namespace`/`-n` flag on any command, or set it permanently with `kubectl config set-context --current --namespace=<name>`
- **Delete:** `kubectl delete namespace <name>` — this cascades and deletes every object inside it

## Key Takeaway
The Pod is Kubernetes' fundamental unit of execution, and almost every other primitive builds on top of it. Knowing how to create, inspect, configure, and clean up Pods — and how to scope them correctly with namespaces — is foundational to everything covered in later chapters.

---
**Book:** CKAD Study Guide
**Author:** Benjamin Muschko
**Chapter:** 5 — Pods and Namespaces (pp. 43–57)