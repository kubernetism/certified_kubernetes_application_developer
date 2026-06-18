# Chapter 9: Labels and Annotations — Questions (Sample Exercises)

> Solutions to these exercises are available in Appendix A.

**1.** Create three Pods that use the image `nginx:1.25.1`. The names of the Pods should be `pod-1`, `pod-2`, and `pod-3`.
- Assign the label `tier=frontend` to `pod-1` and the label `tier=backend` to `pod-2` and `pod-3`. All pods should also assign the label `team=artemidis`.
- Assign the annotation with the key `deployer` to `pod-1` and `pod-3`. Use your own name as the value.
- From the command line, use label selection to find all Pods with the team `artemidis` or `aircontrol` and that are considered a backend service.

**2.** Create a Pod with the image `nginx:1.25.1` that assigns two recommended labels: one for defining the application name with the value `F5-nginx`, and one for defining the tool used to manage the application named `helm`.
- Render the assigned labels of the Pod object.

---
**Book:** CKAD Study Guide
**Author:** Benjamin Muschko
**Chapter:** 9 — Labels and Annotations (pp. 95–104)