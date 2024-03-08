
### Create the pods with below configuration

```html
#### without label
apiVersion: v1
kind: Pod
metadata:
  name: no-label-demo
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```
```html
#### with one label
apiVersion: v1
kind: Pod
metadata:
  name: single-label-demo
  labels:
    app: nginx
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```
```html
#### with multiple labels
apiVersion: v1
kind: Pod
metadata:
  name: multi-labels-demo
  labels:
    app: nginx
    env: dev
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```
![imp_pod_1.png](../assets/imp_pod_1.png)

![imp_pod_2.png](../assets/imp_pod_2.png)
### Display the pod label
`kubectl get pods --show-labels`

![imp_pod_3.png](../assets/imp_pod_3.png)

### Filtering the pods based on the label
`kubectl get pods -l <key=value>`

![imp_pod_4.png](../assets/imp_pod_4.png)

### Adding the labels to the pods
`kubectl label pods <podname> <key=value>`

![imp_pod_5.png](../assets/imp_pod_5.png)

### Overwrite existing labels in the pods
`kubectl label pods <podname> <key=value> --overwrite`

![imp_pod_6.png](../assets/imp_pod_6.png)

###Remove the labels from the pods
`kubectl label pods <podname> key-`

![imp_pod_7.png](../assets/imp_pod_7.png)

###Destroy the pods based on label
`kubectl delete pods -l <key=value>`

![imp_pod_8.png](../assets/imp_pod_8.png)
`Note: When deleting the pod based on the label, it will delete all the pods if the label exists in the pod configuration.`

 <mark>For example, Assume the pod contains 3 labels.Out of 3 labels, only 1 label matches while executing delete command, 
 then this pod will be deleted. </mark>
 
###Label selector - Highlevel

![k8s_label_selector.png](../assets/k8s_label_selector.png)

###Create Deployment
`kubectl create deployment <deployment name> --image=<image name>`

`kubectl create deployment <deployment name> --image=<image name> --replicas=<number of pods>`

![imp_dep_2.png](../assets/imp_dep_2.png)

Below two commands will not create deployment. Instead, it will evaluate if this command can create deployment. If it creates, what would be the yaml file content
`kubectl create deployment <deployment name> --image=<image name> --replicas=<number of pods> --dry-run=client`

`kubectl create deployment <deployment name> --image=<image name> --replicas=<number of pods> --dry-run=client -o yaml`

![imp_dep_1.png](../assets/imp_dep_1.png)

###Change the image in the existing deployment
`kubectl set image deployment <deployment name> <container-name>>=<image name>`

![imp_dep_17.png](../assets/imp_dep_17.png)

###Rolling Status for a deployment and rolling history for a deployment
`kubectl rollout status deployment <deployment name>`

`kubectl rollout history deployment <deployment name>`

![imp_dep_18.png](../assets/imp_dep_18.png)

###Rolling Back  to previous deployment

`kubectl rollout undo deployment <deployment name>`

![imp_dep_16.png](../assets/imp_dep_16.png)

### Rolling Back to particular revision

`kubectl rollout undo deployment <deployment name> --to-revision=<revision number>`

![imp_dep_15.png](../assets/imp_dep_15.png)

### Scaling the deployment

`kubectl scale deployment <deployment name> --replicas=<number of pods>`

![imp_dep_19.png](../assets/imp_dep_19.png)

### Autoscaling the deployment based on CPU usage

`kubectl autoscale deployment <deployment name> --min=2 --max=6 --cpu-percent=<percentage number>`

![imp_dep_20.png](../assets/imp_dep_20.png)

