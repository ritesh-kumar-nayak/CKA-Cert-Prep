## Task 9/40


In this exercise, you will create a Deployment and expose a container port for its Pods. You will demonstrate the differences between the service types ClusterIP and NodePort.

> [!NOTE]
> If you do not already have a Kubernetes cluster, you can create a local Kubernetes cluster by following [Day06 Video](https://youtu.be/RORhczcOrWs)
> Also, do the node binding at the cluster level if you are using KIND. The Day9 video has the details on how to do that.

### Task details
1. Create a Service named `myapp` of type `ClusterIP` that exposes port 80 and maps to the target port 80.
    **Answer**: myapp-svc.yaml
2. Create a Deployment named `myapp` that creates 1 replica running the image `nginx:1.23.4-alpine`. Expose the container port 80.
    **Answer**: myapp-deploy.yaml

3. Scale the Deployment to 2 replicas.
    **Answer**: instead of updating the deployment I used this command `kubectl edit deploy/myapp`

4. Create a temporary Pod using the image `busybox` and run a `wget` command against the IP of the service.
5. Run a `wget` command against the service outside the cluster.
    **Answer**: This will not connect becauseas of now we have created ClusterIP. To connect via wget we need to have NodePort service.
6. Change the service type so the Pods can be reached outside the cluster.
    **Answer**:  type shold be changed to NodePort and nodePort value has to be assigned based on the available ports
        `type: NodePort
        ports:
            - nodePort: 30001`
7. Run a `wget` command against the service outside the cluster.
    **Answer**:  index.html has been downloaded.
    
8. Discuss: Can you expose the Pods as a service without a deployment?
9. Discuss: Under what condition would you use the service types `LoadBalancer,` `node port,` `clusterIP,` and `external`?