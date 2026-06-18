# Chapter 7: Volumes — Questions (Sample Exercises)

> Solutions to these exercises are available in Appendix A.

**1.** Create a Pod YAML manifest with two containers that use the image `alpine:3.12.0`. Provide a command for both containers that keep them running forever. Define a Volume of type `emptyDir` for the Pod. Container 1 should mount the Volume to path `/etc/a`, and container 2 should mount the Volume to path `/etc/b`.
- Open an interactive shell for container 1 and create the directory `data` in the mount path. Navigate to the directory and create the file `hello.txt` with the contents "Hello World." Exit out of the container.
- Open an interactive shell for container 2 and navigate to the directory `/etc/b/data`. Inspect the contents of file `hello.txt`. Exit out of the container.

**2.** Create a PersistentVolume named `logs-pv` that maps to the hostPath `/var/logs`. The access mode should be ReadWriteOnce and ReadOnlyMany. Provision a storage capacity of 5Gi. Ensure that the status of the PersistentVolume shows `Available`.
- Create a PersistentVolumeClaim named `logs-pvc`. It uses ReadWriteOnce access. Request a capacity of 2Gi. Ensure that the status of the PersistentVolume shows `Bound`.
- Mount the PersistentVolumeClaim in a Pod running the image `nginx` at the mount path `/var/log/nginx`.
- Open an interactive shell to the container and create a new file named `mynginx.log` in `/var/log/nginx`. Exit out of the Pod.
- Delete the Pod and re-create it with the same YAML manifest. Open an interactive shell to the Pod, navigate to the directory `/var/log/nginx`, and find the file you created before.

---
**Book:** CKAD Study Guide
**Author:** Benjamin Muschko
**Chapter:** 7 — Volumes (pp. 69–81)