# Practicing and Practice Exams

Hands-on practice is extremely important when it comes to passing the exam. For that purpose, you'll need a functioning Kubernetes cluster environment. The following options stand out:

- I found it useful to run one or many virtual machines using Vagrant and VirtualBox. Those tools help with creating an isolated Kubernetes environment that is easy to bootstrap and dispose on demand.
- It is relatively easy to install a simple Kubernetes cluster on your developer machine. The Kubernetes documentation provides various installation options, depending on your operating system. Minikube is useful when it comes to experimenting with more advanced features like Ingress or storage classes, as it provides the necessary functionality as add-ons that can be installed with a single command. Alternatively, you can also give kind a try, another tool for running local Kubernetes clusters.
- If you're a subscriber to the O'Reilly Learning Platform, you have unlimited access to scenarios running a Kubernetes sandbox environment. In addition, you can test your knowledge with the help of the CKAD practice test in the form of interactive labs.

You may also want to try one of the following commercial learning and practice resources:

- Killer Shell is a simulator with sample exercises for all Kubernetes certifications. If you purchase a voucher for the exam, you will be allowed two free sessions.
- Other online training providers offer video courses for the exam, some of which include an integrated Kubernetes practice environment. I would like to mention KodeKloud and A Cloud Guru. You'll need to purchase a subscription to access the content for each course individually.

## Summary

The exam is a completely hands-on test that requires you to solve problems in multiple Kubernetes clusters. You're expected to understand, use, and configure the Kubernetes primitives relevant to application developers. The exam curriculum subdivides those focus areas and puts different weights on topics, which determines their contributions to the overall score. Even though focus areas are grouped meaningfully, the curriculum doesn't necessarily follow a natural learning path, so it's helpful to cross-reference chapters in the book in preparation for the exam.

In this chapter, we discussed the exam environment and how to navigate it. The key to acing the exam is intense practice of kubectl to solve real-world scenarios. The next two chapters in Part I will provide a jump start to Kubernetes. All chapters that discuss domain details give you an opportunity to practice hands-on. You will find sample exercises at the end of each chapter.

---

# Command-Line Tips and Tricks

Given that the command line is your solitary interface to the Kubernetes cluster, it's essential that you become extremely familiar with the kubectl tool and its available options. This section provides tips and tricks for making their use more efficient and productive.

## Setting a Context and Namespace

The exam environment comes with multiple Kubernetes clusters already set up for you. Take a look at the instructions for a high-level, technical overview of those clusters. Each of the exam exercises needs to be solved on a designated cluster, as outlined in its description. Furthermore, the instructions will ask you to work in a namespace other than default. Make sure to set the context and namespace as the first course of action before working on a question. The following command sets the context and the namespace as a one-time action:

```bash
$ kubectl config set-context <context-of-question> \
  --namespace=<namespace-of-question>
$ kubectl config use-context <context-of-question>
```

You can find a more detailed discussion of the context concept and the corresponding kubectl commands in "Authentication with kubectl" on page 188.

## Using the Alias for kubectl

In the course of the exam, you will have to execute the kubectl command tens or even hundreds of times. You might be an extremely fast typist; however, there's no point in fully spelling out the executable over and over again. The exam environment already sets up the alias `k` for the kubectl command. In preparation for the exam, you can set up the same behavior on your machine. The following alias command maps the letter `k` to the full kubectl command:

```bash
$ alias k=kubectl
$ k version
```

## Using kubectl Command Auto-Completion

Memorizing kubectl commands and command-line options takes a lot of practice. The exam environment comes with auto-completion enabled by default. You can find instructions for setting up auto-completion for the shell on your machine in the Kubernetes documentation.

## Internalize Resource Short Names

Many of the kubectl commands can be quite lengthy. For example, the command for managing Persistent Volume Claims is `persistentvolumeclaims`. Spelling out the full command can be error-prone and time-consuming. Thankfully, some of the longer commands come with a short-form usage. The command `api-resources` lists all available commands plus their short names:

```bash
$ kubectl api-resources
NAME                    SHORTNAMES  APIGROUP  NAMESPACED  KIND
...
persistentvolumeclaims  pvc                   true        PersistentVolumeClaim
...
```

Using `pvc` instead of `persistentvolumeclaims` results in a more concise and expressive command execution, as shown here:

```bash
$ kubectl describe pvc my-claim
```

---

## Exercises

### Exercise 1 — Setting Context and Namespace

You are given a cluster context named `ckad-practice` and need to work in a namespace called `dev-team`.

1. Write the two `kubectl` commands required to set the context to `ckad-practice` with namespace `dev-team` and then switch to that context.
2. After switching, run a command to verify which context is currently active.

<details>
<summary>Solution</summary>

```bash
# Step 1: Set the context with namespace
$ kubectl config set-context ckad-practice --namespace=dev-team

# Step 2: Switch to the context
$ kubectl config use-context ckad-practice

# Step 3: Verify the active context
$ kubectl config current-context
```

</details>

---

### Exercise 2 — Creating the kubectl Alias

You want to avoid typing `kubectl` in full during the exam.

1. Create an alias `k` that maps to `kubectl`.
2. Use the alias to check the Kubernetes client and server version.

<details>
<summary>Solution</summary>

```bash
# Step 1: Set the alias
$ alias k=kubectl

# Step 2: Verify using the alias
$ k version
```

> **Tip:** To make the alias persistent across sessions, add `alias k=kubectl` to your `~/.bashrc` or `~/.zshrc` file.

</details>

---

### Exercise 3 — Enabling kubectl Auto-Completion

Auto-completion saves time and reduces typos.

1. Enable `kubectl` bash auto-completion for the current shell session.
2. Make it persistent by adding it to your shell config file.
3. If you have the alias `k` set, also enable auto-completion for `k`.

<details>
<summary>Solution</summary>

```bash
# Step 1: Enable for current session
$ source <(kubectl completion bash)

# Step 2: Make it persistent
$ echo "source <(kubectl completion bash)" >> ~/.bashrc

# Step 3: Enable completion for alias k
$ echo "complete -F __start_kubectl k" >> ~/.bashrc

# Reload the shell config
$ source ~/.bashrc
```

</details>

---

### Exercise 4 — Discovering and Using Resource Short Names

1. Run the command to list all available Kubernetes API resources along with their short names.
2. Identify the short name for the following resources:
   - `persistentvolumeclaims`
   - `configmaps`
   - `serviceaccounts`
   - `namespaces`
3. Use the appropriate short name to describe a PersistentVolumeClaim named `data-claim`.

<details>
<summary>Solution</summary>

```bash
# Step 1: List all API resources with short names
$ kubectl api-resources

# Step 2: Short names
# persistentvolumeclaims → pvc
# configmaps             → cm
# serviceaccounts        → sa
# namespaces             → ns

# Step 3: Describe the PVC using short name
$ kubectl describe pvc data-claim
```

</details>

---

### Exercise 5 — Putting It All Together

Simulate the start of a real CKAD exam question:

1. Set and switch to a context named `cluster-1` with namespace `production`.
2. Using the `k` alias and short names, list all Pods and all PersistentVolumeClaims in the `production` namespace.
3. Describe the PVC named `app-storage` using its short name.

<details>
<summary>Solution</summary>

```bash
# Step 1: Set context and namespace
$ kubectl config set-context cluster-1 --namespace=production
$ kubectl config use-context cluster-1

# Step 2: Set alias (if not already set)
$ alias k=kubectl

# List Pods
$ k get pods

# List PVCs using short name
$ k get pvc

# Step 3: Describe the specific PVC
$ k describe pvc app-storage
```

</details>