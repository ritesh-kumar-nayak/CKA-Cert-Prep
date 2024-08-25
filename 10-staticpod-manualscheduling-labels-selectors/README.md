### Static Pod
Static pod is a pod which is not managed by the **Scheduler**. Usually all the pods that are supposed to be creaed are managed by Scheduler and scheduler makes sure that the pod is being created in particular node.

Static Pods are managed by **Kubelet**

**Kubelete**: the kubelet runs on each node in the Kubernetes cluster and is responsible for managing the containers on that specific node. It ensures that containers defined in the PodSpecs are running on the node and maintains their lifecycle, including monitoring, restarting, and reporting status to the Kubernetes control plane.

**Scheduler**: The kube-scheduler is a central component that runs as part of the Kubernetes control plane. The kube-scheduler makes scheduling decisions based on resource availability, affinity/anti-affinity rules, taints, tolerations, and other constraints to ensure that the pod is placed on the most suitable node.

**Static Pod Manifests** are stored in `/etc/kubernetes/manifests` directory on controll plane node.

# Manual Scheduling
Manual Scheduling is when we want our pod to be scheduled on a specific node of our choice. This can be done by adding a nodeName attribute in the pod as explained below.

Manual scheduling is important when there is any issue  with scheduler. It basically eliminates the job of a scheduler at the time of pod creation as we have declared the node name already
### # nodeName attribute

When a nodeName attribute is specified in a pod manifest, scheduler does not worry about the pod anymore as we have already defined on whihc node this particular pod will be created.

In the below pod manifest we have scheduled explicitly specified on which worker-node the pod should be created

`apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
  nodeName: ckacluster1-worker2`

# Labels and Selectors
Labels and selectors are nothing but tags that are used to group and identify deployments, pods and other components.
It helps us filter kubernetes objects based on tags when we are dealing with lots of pods and objects. Below command can be used to filter them.

`kubectl get pod --selectors env=demo`