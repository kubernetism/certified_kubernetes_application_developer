# Chapter 3: Interacting with Kubernetes — Summary

## API Primitives and Objects
Kubernetes primitives (Pod, Deployment, Service, etc.) act like classes in object-oriented programming — they are blueprints. A Kubernetes *object* is an instance of a primitive, complete with its own system-generated unique identifier (UID). Every object manifest follows a general structure: **apiVersion**, **kind**, **metadata**, **spec**, and **status**.

- **apiVersion** — defines the schema/structure used to validate the object.
- **kind** — the type of primitive (e.g., Pod, Service).
- **metadata** — name, namespace, labels, annotations, and UID.
- **spec** — the desired state of the object.
- **status** — the actual, current state, continuously reconciled toward the spec by Kubernetes controllers.

## Using kubectl
kubectl is the primary, exam-required CLI tool for interacting with a cluster. Its general syntax is:

```
kubectl [command] [TYPE] [NAME] [flags]
```

Resource types can be referenced by full name or short form (e.g., `svc` for `service`). Object names must be unique within a namespace and are distinct from the internal UID.

## Managing Objects
Kubernetes objects can be managed two ways:

### Imperative Object Management
Objects are created/updated/deleted directly via single kubectl commands without a manifest file.
- **Create:** `kubectl run` or `kubectl create`
- **Update:** `kubectl edit` (opens the live config in an editor) or `kubectl patch` (JSON merge patch for fine-grained changes)
- **Delete:** `kubectl delete`, optionally with `--now` to force immediate (SIGKILL) termination instead of waiting out the default 30-second grace period

This approach is fast and ideal for quick changes or exam scenarios, but doesn't scale well for complex, auditable configurations.

### Declarative Object Management
Objects are defined in YAML/JSON manifests and managed with `kubectl apply -f`, which can point to a single file, a directory, a recursive directory tree, or even an HTTP(S) URL. Re-running `apply` after editing a manifest synchronizes the live object with the new desired state. Kubernetes tracks this via the `kubectl.kubernetes.io/last-applied-configuration` annotation. Deleting declaratively-managed objects is best done with `kubectl delete -f <file>`.

This approach is reproducible, version-controllable, and recommended for production. It's also the foundation of **GitOps**, where tools like Argo CD and Flux apply manifests from Git repositories automatically.

### Hybrid Approach
You can generate a YAML manifest from an imperative command without creating the object, using `-o yaml --dry-run=client`, then hand-edit the file before applying it declaratively. This combines the speed of imperative commands with the structure of declarative manifests.

### Which Approach to Use?
During the exam, imperative commands are fastest. In real-world production environments, the declarative approach is preferred for traceability, collaboration, and version control.

## Key Takeaway
Kubernetes objects always have a desired state (spec) that the system continuously reconciles toward the actual state (status). kubectl is the exclusive client used for both imperative, fast, single-command operations and declarative, manifest-driven, production-grade operations — knowing when to use each is core to working efficiently with Kubernetes.

---
**Book:** CKAD Study Guide
**Author:** Benjamin Muschko
**Chapter:** 3 — Interacting with Kubernetes (pp. 21–30)