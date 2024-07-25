## Task 7/40


1. **Task Details** ☕️
**Task 1**
- Create a pod using the imperative command and use nginx as the image
    Answer: kubectl run nginx --image=nginx:latest

**Task2**
- Create the YAML from the nginx pod created in task 1

    Answer: kubectl run nginx --image=nginx:latest --dry-run=client -o yaml > task2.yml

- Update the pod name in the YAML
    Answer: task2.yml

- Use that YAML to create a new pod with the name nginx-new.
    Answer: kubectl create -f task2.yml

**Task3**
- Apply the below YAML and fix the errors, including all the commands that you run during the troubleshooting and the error message

    Answer:  kubectl describe pod redis
            Error: "Normal   BackOff    2m8s (x4 over 3m10s)  kubelet            Back-off pulling image "rediss"
                    Warning  Failed     2m8s (x4 over 3m10s)  kubelet            Error: ImagePullBackOff
                    Normal   Pulling    113s (x4 over 3m14s)  kubelet            Pulling image "rediss"
                    Warning  Failed     109s (x4 over 3m11s)  kubelet            Failed to pull image "rediss": failed to pull and unpack image "docker.io/library/rediss:latest": failed to resolve reference "docker.io/library/rediss:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed"

```YAML
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: test
  name: redis
spec:
  containers:
  - image: rediss
    name: redis
    
