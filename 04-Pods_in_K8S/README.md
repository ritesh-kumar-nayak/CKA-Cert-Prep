# POD
# ===
As we know pod is the smallest component of Kubernets. 
There are 2 way of creating a pod:
    i) Imperative 
    ii) Declarative
# Imperative
# ===========
Imperative way is when you run a pod using kubectl ad-hoc commands.
Example: 
Create a Nginx pod through kubectl imperative way: kubectl run nginx-pod --image=nginx:latest

# Declarative
# ===========
Declarative way is when you define you desired state of a pod in a manifest file which can be written in YAML or JSON and then 
run "kubectl create" or apply command on those YAML manifests.
YAML is the most used language for creating any manifest file in Kubernetes.

Once manifest file is created you can you below commands to apply the configuration:
 kubectl create -f file_name.yml
 OR
 `kubectl apply -f file_name.yml`
 NB: the apply command is mostly used when there is any changes in an existing configuration.


# Creating Manifest files Smartly
# ===============================
We do not need to remember everything about creating the manifestfile via declarative way, we can genenerate the file using the imerative commands as below:
   
    `kubectl run container_name --image=image_name:tag --dry-run=client -o yaml > file_name.yaml`

  # Example:
    kubectl run nginx --image=nginx --dry-run=client -o yaml > pod_via_imperative.yaml
    Now the file named "pod_via_imperative.yaml" is created by the above command.

# "kubectl explain" Command
==============================
This command is used to get the details of any kubernetes objects such as pod, node etc when writing manifest files in the declarative way.

Example: kubectl explain pod
         kubectl explain node
         kubectl explain deployment
         kubectl explain replicaset
         kubectl explain service



### Troublshooting Commands:
`kubectl get nodes` : it lists down the nodes with basic details

`kubectl get nodes -o wide` : it shows the list of pods with additional details such as INTERNAL-IP, EXTERNAL-IP, OS-IMAGE, KERNEL-VERSION, CONTAINER-RUNTIME

`kubectl get pods` : it lists down the pods with basic details

`kubectl get pods -o wide` : it shows the list of pods with additional details such as node and IP

`kubectl describe pod pod_name` : it gives a detailed information about pod inclding which node it runs, ports, namepaces etc..

`kubectl exec -it pod_name --sh` : it gives the access to pod's shell in an interactive mode

`kubectl edit pod pod_name` : it allows you to edit the configuration of a running or inactive pod directly instead of doing so via yaml file

`kubectl get pods pod_name --show-labels` : it shows pod labels


