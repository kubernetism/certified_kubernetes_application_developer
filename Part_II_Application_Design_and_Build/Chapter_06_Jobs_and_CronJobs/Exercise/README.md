# Chapter 6: Jobs and CronJobs — Questions (Sample Exercises)

> Solutions to these exercises are available in Appendix A.

**1.** Create a Job named `random-hash` using the container image `alpine:3.17.3` that executes the shell command `echo $RANDOM | base64 | head -c 20`. Configure the Job to execute with two Pods in parallel. The number of completions should be set to 5.
- Identify the Pods that executed the shell command. How many Pods do you expect to exist?
- Retrieve the generated hash from one of the Pods.
- Delete the Job. Will the corresponding Pods continue to exist?

**2.** Create a new CronJob named `google-ping`. When executed, the Job should run a `curl` command for google.com. Pick an appropriate image. The execution should occur every two minutes.
- Watch the creation of the underlying Jobs managed by the CronJob. Check the command-line options of the relevant command or consult the Kubernetes documentation.
- Reconfigure the CronJob to retain a history of seven executions.
- Reconfigure the CronJob to disallow a new execution if the current execution is still running. Consult the Kubernetes documentation for more information.

---
**Book:** CKAD Study Guide
**Author:** Benjamin Muschko
**Chapter:** 6 — Jobs and CronJobs (pp. 59–67)