# Chapter 7: Volumes — Summary

## Why Volumes Exist
A container's temporary filesystem is isolated and disappears on restart — anything written there is lost. A Pod can define a Volume and mount it into a container so data survives beyond the container's own lifecycle.

## Volume Types
- **Ephemeral Volumes** — last only for the Pod's lifespan. Useful for sharing data between containers in the same Pod, or for easily-reconstructed data.
- **Persistent Volumes** — outlive the Pod, good for things like database storage.

Notable types: `emptyDir` (empty read/write directory, lifespan of the Pod — great for caches or inter-container exchange), `hostPath` (mounts a path from the host node — single-node/dev only, not for production), `configMap`/`secret` (inject config data), `nfs` (network share, survives Pod restarts), and `persistentVolumeClaim` (claims a PersistentVolume).

**Defining and mounting an ephemeral Volume** requires two steps: declare it under `spec.volumes[]` (name + type), then mount it into a container via `spec.containers[].volumeMounts[]`, matched by name.

## Persistent Volumes (PV) and Claims (PVC)
A **PersistentVolume** represents an actual piece of cluster storage, fully decoupled from any Pod's lifecycle. It can be provisioned **statically** (an admin manually creates a `PersistentVolume` object — `kubectl` has no `create` shortcut for this, only the manifest-first approach) or **dynamically** (auto-created from a `PersistentVolumeClaim` via a `StorageClass`).

Key PV configuration options:
- **Volume mode** (`spec.volumeMode`) — `Filesystem` (default) or `Block`.
- **Access mode** (`spec.accessModes`) — `ReadWriteOnce` (RWO), `ReadOnlyMany` (ROX), `ReadWriteMany` (RWX), `ReadWriteOncePod` (RWOP).
- **Reclaim policy** — `Retain` (default, keeps the PV after its claim is deleted), `Delete` (removes the PV and its storage), `Recycle` (deprecated).

A **PersistentVolumeClaim** requests storage (size + access mode) from a PV. The binding between a PVC and a PV is strictly one-to-one. Once bound, you mount the claim into a Pod via `spec.volumes[].persistentVolumeClaim.claimName` — the same pattern used for any other Volume type.

## Storage Classes
A **StorageClass** defines a "class" of storage (e.g., fast SSD vs. slower remote storage) and is what enables *dynamic* provisioning — you don't create the PV yourself; the class's provisioner does it for you when a matching PVC requests it. A StorageClass needs at minimum a `provisioner`; everything else has sane defaults. Assign one to a PVC via `spec.storageClassName`. If no matching PV can be provisioned, Kubernetes does **not** raise an error — worth remembering for debugging.

## Key Takeaway
Ephemeral Volumes solve the "containers in a Pod need to share files" problem; Persistent Volumes solve the "data needs to outlive the Pod entirely" problem. PVCs are the abstraction layer that lets a Pod request storage without caring whether it was provisioned statically by an admin or dynamically by a StorageClass.

---
**Book:** CKAD Study Guide
**Author:** Benjamin Muschko
**Chapter:** 7 — Volumes (pp. 69–81)