# Chapter 5: Pods and Namespaces — Questions (Sample Exercises)

> Solutions to these exercises are available in Appendix A.

**1.** Create a new Pod named `nginx` running the image `nginx:1.17.10`. Expose the container port 80. The Pod should live in the namespace named `ckad`.
- Get the details of the Pod including its IP address.
- Create a temporary Pod that uses the `busybox:1.36.1` image to execute a `wget` command inside of the container. The wget command should access the endpoint exposed by the nginx container. You should see the HTML response body rendered in the terminal.
- Get the logs of the nginx container.
- Add the environment variables `DB_URL=postgresql://mydb:5432` and `DB_USERNAME=admin` to the container of the nginx Pod.
- Open a shell for the nginx container and inspect the contents of the current directory `ls -l`. Exit out of the container.

**2.** Create a YAML manifest for a Pod named `loop` that runs the `busybox:1.36.1` image in a container. The container should run the following command: `for i in {1..10}; do echo "Welcome $i times"; done`. Create the Pod from the YAML manifest. What's the status of the Pod?
- Edit the Pod named `loop`. Change the command to run in an endless loop. Each iteration should echo the current date.
- Inspect the events and the status of the Pod `loop`.

---
**Book:** CKAD Study Guide
**Author:** Benjamin Muschko
**Chapter:** 5 — Pods and Namespaces (pp. 43–57)