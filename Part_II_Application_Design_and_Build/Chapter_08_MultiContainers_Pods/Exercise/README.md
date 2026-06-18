# Chapter 8: Multi-Container Pods — Questions (Sample Exercises)

> Solutions to these exercises are available in Appendix A.

**1.** Create a YAML manifest for a Pod named `complex-pod`. The main application container named `app` should use the image `nginx:1.25.1` and expose the container port 80. Modify the YAML manifest so that the Pod defines an init container named `setup` that uses the image `busybox:1.36.1`. The init container runs the command `wget -O- google.com`.
- Create the Pod from the YAML manifest.
- Download the logs of the init container. You should see the output of the `wget` command.
- Open an interactive shell to the main application container and run the `ls` command. Exit out of the container.
- Force-delete the Pod.

**2.** Create a YAML manifest for a Pod named `data-exchange`. The main application container named `main-app` should use the image `busybox:1.36.1`. The container runs a command that writes a new file every 30 seconds in an infinite loop in the directory `/var/app/data`. The filename follows the pattern `{counter++}-data.txt`. The variable counter is incremented every interval and starts with the value 1.
- Modify the YAML manifest by adding a sidecar container named `sidecar`. The sidecar container uses the image `busybox:1.36.1` and runs a command that counts the number of files produced by the `main-app` container every 60 seconds in an infinite loop. The command writes the number of files to standard output.
- Define a Volume of type `emptyDir`. Mount the path `/var/app/data` for both containers.
- Create the Pod. Tail the logs of the sidecar container.
- Delete the Pod.

---
**Book:** CKAD Study Guide
**Author:** Benjamin Muschko
**Chapter:** 8 — Multi-Container Pods (pp. 83–94)