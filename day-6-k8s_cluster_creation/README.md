### Most Important Kubernetes Reference Links:
[kubectl sheatsheet](https://kubernetes.io/pt-br/docs/reference/kubectl/cheatsheet/)
[Kubernetes Docs](https://kubernetes.io/pt-br/docs/reference/)


### K8S installation and Setup
We'll be using "Kind" application for our learning purpose.
Kind is a application that will help us creating K8S clusters( Single node cluster and multi-node cluster ) through out our preparation

[Kind Installation and configuration](https://kind.sigs.k8s.io/docs/user/quick-start/#installing-with-a-package-manager)

## Creating a single cluster

# Syntax: 
kind create cluster --image kubernetes_image --name name_for_your_cluster
# Example:
kind create cluster --image kindest/node:v1.30.0@sha256:047357ac0cfea04663786a612ba1eaba9702bef25227a794b52890dd8bcd692e --name ckacluster1

[You can get the kubernetes images for Kind from here](https://github.com/kubernetes-sigs/kind/releases)

## Creating Multi-Node Cluster
To create a multi-node cluster, kind requirs a config.yaml file which is also provided in the same documentation above.
We'll keep this yaml file in this directory.

# Syntax:
kind create cluster --config kind-example-config.yaml

# Example: 
kind create cluster --config kind_k8s_config.yaml

OR

kind create cluster --image kindest/node:v1.30.0@sha256:047357ac0cfea04663786a612ba1eaba9702bef25227a794b52890dd8bcd692e --name ckacluster2 --config kind_k8s_config.yaml

### kubectl Installation

When a K8s cluster is created we can interact with the cluster using "kubectl" command line.
"kubectl" utility needs to be installed beforw creating any kubernetes cluster.

[Install Kubectl](https://kubernetes.io/docs/tasks/tools/)

# kubectl get nodes: gives details of nodes

NB: When a cluster is created and we run "kubectl get node" it provides the node details of newly created node as kubectl gets auto-switched to the latest node.

# kubectl config get-contexts : Lists the available clusters

This config get-contexts command is used to list the active clusters and shows on which cluster you are currently in.

## Example of output
 kubectl config get-contexts
CURRENT   NAME               CLUSTER            AUTHINFO           NAMESPACE
          kind-ckacluster1   kind-ckacluster1   kind-ckacluster1
*         kind-ckacluster2   kind-ckacluster2   kind-ckacluster2


# kubectl config use-context cluster_name : switch to your required cluster

This config use-context will be used to switch to any available cluster you want to switch to.
* mark defines on which cluster you are currently in.

## Example of output

 kubectl config use-context kind-ckacluster1
Switched to context "kind-ckacluster1".
