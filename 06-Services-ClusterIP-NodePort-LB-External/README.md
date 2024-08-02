There mainly 3 types of services in Kubernetes:

    1. NodePort : it is used to expose the application to outside
    2. ClusterIp : It is used for inter-pod communication
    3. LoadBalancer : it is a service type which takes care of loadbalancing keeping all the pods behind it. It has a loadbalancing algorithm.



# Get the service details
**Command**: `kubectl get svc`
Once servuce is created it should be accessible at <NodePortIp>:<port>
Exaple: 172.23.0.2:30001 ( This will work in normal kubernetes cluster )


However, as we are using Kind cluster instead of normal Kubernetes cluster we have to do an additional step in Kind Configuration.

`kubectl get endpoints` is used to list down the endpoints of a service.

**Endpoints**: Endpoint is nothing but the `IPs:port` of the pods running inside the cluster. This endpoint gets updated
everytime a pod is recreated.2

**Command to generate NodePort svc**:
kubectl expose deployment <deployment-name> --type=NodePort --port=<service-port> --target-port=<container-port> --dry-run=client -o yaml > nodeport-service.yaml

Example: kubectl expose deployment my-deployment --type=NodePort --port=80 --target-port=8080 --dry-run=client -o yaml > nodeport-service.yaml