### DaemonSet
A daemonset in kubernetes is a resource that ensures a copy of a specific pod is running on all available nodes in k8s.
This is particularly useful for running background task or system service that need to be present on every node.

**Everytime a new node is created DaemonSet detects it and creates a pod inside it**
**Few default pods that are run by DS are below:**
    Monitoring Agent
    kube-proxy
    weave-net
    Flannel etc..

In DaemonSet we do not need to declare the number of replicas. DS automatically creates a replica in each available node.
`kubectl explain daemonset`: this will give the explaination of DS
`kubectl get ds -A` : displays all the daemonsets across the namespace.

### Cron Job
Cron job is a task that executes on a scheduled time.
### Job
It does not execute on scheduled time. It executes once and completes the task.