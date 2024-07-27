# ReplicationController & ReplicaSet

Replication Controller and ReplicaSet are both controllers in Kubernetes that ensure the desired number of pod replicas are running at any given time. However, ReplicaSet is the more advanced and preferred controller as of Kubernetes 1.2, with some improvements over the older Replication Controller.

### Replication Controller
A Replication Controller ensures that a specified number of pod replicas are running at any given time. If there are too many pods, it will kill some; if there are too few, it will start more. This makes it a key tool for maintaining high availability and ensuring that your application can handle the desired load.

### ReplicaSet
A ReplicaSet is the next-generation Replication Controller. It also ensures that a specified number of pod replicas are running, but it introduces new features and improvements.

# How They Work Together
### Standalone Use:
    Replication Controller: Ensures a specified number of pods are running and can be used directly.
    ReplicaSet: Provides a similar function but with more advanced label selection. It can also be used directly.
### Deployment Management:
    Deployments use ReplicaSets to manage the desired state of the application.
    When you create or update a Deployment, it creates or updates the associated ReplicaSet, which in turn manages the pods.
### Use with Deployments:
    Replication Controllers are not typically used with Deployments.
    ReplicaSets are the underlying mechanism used by Deployments to manage pods.

# ReplicationController vs ReplicaSet

    RC is used to manage resources(Pods) that are created as part of that particular ReplicaController 
    
    With ReplicaSet(RS) we can even manage pods that were not created by that particular ReplicaSet initially. We can achieve that with the help of another field called "selector" and inside that "matchLabels". 
    Here under matchLabels we put  the labels defined in pod so that any pod created with that label will be associated and managed by this particular ReplicaSet.

# Deployment
A Deployment in Kubernetes is a higher-level abstraction that manages a group of identical pods using ReplicaSets. It provides declarative updates to applications, allowing you to define the desired state of your application, and the Deployment controller works to match the actual state to the desired state. Deployments offer several advanced features that simplify application management and provide more control over the application lifecycle.

# Key Features of Deployments
### Declarative Updates:

You specify the desired state of your application in a Deployment YAML file, and Kubernetes ensures that this state is maintained.

### Rolling Updates:

Deployments support rolling updates, where old versions of pods are gradually replaced with new versions without downtime. You can control the pace and availability during the update.

### Rollback:

If something goes wrong with an update, you can roll back to a previous version. Kubernetes keeps track of revisions and allows easy rollback to ensure stability.

### Scaling:
You can scale up or scale down the number of pod replicas managed by a Deployment easily, ensuring that your application can handle varying loads.

### Self-Healing:
Deployments monitor the health of pods and automatically replace failed or unresponsive pods to maintain the desired state.

### Automated Rollouts:
Deployments allow automated rollouts of application updates, with the ability to pause, resume, and abort updates based on conditions you define.

# Summary

Deployment Creates ReplicaSet
ReplicaSet Creates Pod

# Commands

   ` kubectl apply -f replica_set.yml` : to create the pod using replica set or apply configuration changes to replicaset
    `kubectl explain rs`  : explains the detail of ReplicaSet such as apiVersion, GROUP etc..
    `kubectl explain rc`  : explains the detail of ReplicationController such as apiVersion, GROUP etc..
    `kubectl explain deploy`   : explains the detail of Deployment such as apiVersion, GROUP etc..

    `kubectl edit rs/name_of_replicaset` : allows you to edit the running ReplicaSet. You can edit anything such as replica count etc..
        Example: kubectl edit rs/nginx-rs
    
    `kubectl scale --replicas=10 rs/name_of_replicaset`   : this is the imperative command to scale up or down
    
    `kubectl delete rs/name_of_replicaset`  : allows you to delete all the resources created by the specified replicaset
    `kubectl delete -f replica_set.yml`   : also allows you to delete all the resources created by the specified replicaset
    `kubectl delete deploy/name_of_deploy`  : allows to delete all the resources created by specified Deployment
    `kubectl set image deploy/nginx-deploy nginx-container=nginx:1.9.1` : updated the image of running nginx container. But you stll have to update the deployment.yml
    ``kubectl set image deploy/name_of_deploy container_name=ngimage:tag``
        Example:  `kubectl set image deploy/nginx-deploy nginx-container=nginx:1.9.1`
    
    `kubectl rollout history deploy/deployment_name` : displays the list of rollouts/changes happened so far
        Example: kubectl rollout history deploy/nginx-deploy
        Output: deployment.apps/nginx-deploy 
                    REVISION  CHANGE-CAUSE
                    1         <none>
                    2         <none>
    `kubectl rollout undo deploy/nginx-deploy`  : Roll back the changed made recently.

