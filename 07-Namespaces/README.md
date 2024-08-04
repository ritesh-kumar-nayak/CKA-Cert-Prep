Namespaces in K8S are logical isolation of resources.

There are multiple ways of creating a namespcase just like services, deployments etc..
    
   ## 1. Declarative way ( Using YAML file )
            Declarative way of creating namespace is where you define the namespace detais in a YAML configuration

            **Command**: `kubectl apply -f namespace.yaml`
                          `kubectl delete -f namespace.yaml` or `kubectl delete ns/demo`

   ## 2.  Imperative way (Using ad-hoc commands)
            This is the simple and easiest and most prefered way of creating a Namespace
            You just need to use below command:
            
            `kubectl create ns <namespaceName>`
           
            `kubectl create ns demo`

`kubectl explain ns`  will help us get the apiVersion and other details of Namespace object in k8s

### Commands:

`kubectl get namespace` : Lists down all the name space
`kubectl get all --namespace`=<name_space_name>
`kubectl get all -n=default `( Instead of --namespace we can use -n )
`kubectl create deploy nginx --image=nginx:latest -n=<namespace_name>`: create a deployment in a particular namespace called demo.
`kubectl get deploy -n <namespace_name>`: get the deployment list of a particular namespace
`kubectl scale --replicas=3 deploy/nginx-demo -n ns-demo` : scale replica of a deployment in a specfic namespace( ns-demo here )
`expose deploy/nginx-demo --name=svc-demo --port=80` : imperative command to expose the service for a deployment