# Chapter 9: Labels and Annotations — Summary

## Labels
Labels are key-value pairs attached to objects so they can be queried, filtered, and sorted later — think of them as tags on a blog post. They're limited to 63 characters and a restricted set of alphanumeric/separator characters. Labels are essential to how higher-level primitives like Deployments, Services, and NetworkPolicies actually function — those objects work by *selecting* a set of Pods via labels.

**Declaring labels** — imperatively with `--labels`/`-l` on `kubectl run` (comma-separated key=value pairs), or declaratively under `metadata.labels` in a manifest.

**Inspecting labels** — `kubectl describe`, `get -o yaml`, or the `--show-labels` flag (adds a `LABELS` column to `get` output).

**Modifying live labels** — `kubectl label pod <name> key=value` to add or change one; add `--overwrite` to replace an existing value; append a trailing `-` to the key (e.g. `region-`) to remove it.

**Label selectors** — used via `--selector`/`-l` on the command line, or `matchLabels`/`matchExpressions` inside a manifest (e.g. a NetworkPolicy's `podSelector`). Two requirement styles:
- **Equality-based** (`=`, `==`, `!=`) — multiple terms combine with a boolean AND.
- **Set-based** (`in`, `notin`, `exists`) — `in`/`notin` evaluate as a boolean OR over the listed values.

Both styles can be combined in a single query.

**Recommended labels** — Kubernetes suggests a standard set prefixed with `app.kubernetes.io/` (e.g. `app.kubernetes.io/version`, `app.kubernetes.io/component`) so tooling and teams share consistent terminology across objects.

## Annotations
Annotations are also key-value pairs, but they exist purely for descriptive, human-readable metadata (commit hashes, release info, contact details) — **they cannot be used to query or select objects**, unlike labels.

**Declaring annotations** — only via a manifest's `metadata.annotations`; `kubectl run` has no equivalent of the `--labels` flag for annotations.

**Modifying live annotations** — `kubectl annotate pod <name> key=value` mirrors the `label` command's syntax exactly, including `--overwrite` and the trailing-`-` removal trick.

**Reserved annotations** — certain annotation keys are interpreted directly by Kubernetes (or its extensions) to control runtime behavior — for example, `pod-security.kubernetes.io/enforce` on a namespace to enforce a Pod Security Standard.

## Key Takeaway
Labels are *functional* — Kubernetes primitives use them to select and act on groups of objects. Annotations are *informational* — they describe an object for humans (or external tooling reading reserved keys) but are invisible to label-based selection. Mixing the two up is a common beginner mistake worth avoiding.

---
**Book:** CKAD Study Guide
**Author:** Benjamin Muschko
**Chapter:** 9 — Labels and Annotations (pp. 95–104)