# Command to Taint
kubectl taint node <node_name> key=value:NoSchedule

Example: `kubectl taint node ckacluster1-worker gpu=true:NoSchedule`
Now, the worker node will only accept the pods which has Toleration as gpu=true

`kubectl describe node ckacluster1-worker2 | grep -i taint` : This command is used to cross check the taint
Taints:             gpu=true:NoSchedule

# Command to Remove Taint
`kubectl taint node ckacluster1-worker2 gpu=true:NoSchedule-`: This command is used to remove taint or untaint a node.

# Command to add Label to a node
kubectl label node <Node_Name> key=value
Example: `kubectl label node  ckacluster1-worker2 gpu=false`


### Taint and Tolerations vs Label
Taint and Toleration help the node to restrict the Pod having mismatched tolerations. Here node choses which pod will be accepted to be scheduled.

Where as, in case of Label, pod decides which node it has to be scheduled based on the attribute "nodeSelector".