## k8s Commands

### Resource Management:

* kubectl create
* kubectl get
* kubectl describe
* kubectl apply
* kubectl delete
* kubectl logs
* kubectl exec
* kubectl port-forward
* kubectl rollout
* kubectl scale

### Configuration Management:

* kubectl cluster-info
* kubectl config
* kubectl rollout history
* kubectl edit
* kubectl label
* kubectl taint
* kubectl annotate
* kubectl exec -it
* kubectl top
* kubectl apply -f
* kubectl config view

### Rollout Management:

* kubectl rollout restart
* kubectl logs --tail
* kubectl rollout undo
* kubectl exec -p
* kubectl rollout status

### Cluster Management:

* kubectl get events

### API Management:

* kubectl api-resources

### Rollout Management:

* kubectl rollout pause
* kubectl rollout resume

### Resource Deletion:

* kubectl delete pod --force

### Resource Configuration:

* kubectl explain

---
### kubectl create:


The kubectl create command is used to create new Kubernetes resources. For example, you can create a new deployment, service, or pod using this command. Here's an example of how to create a new deployment:
```bash
kubectl create deployment nginx --image=nginx
```

> This command creates a new deployment named nginx using the official nginx Docker image. You can then use the kubectl get command to see the status of the deployment.

### kubectl get:
The kubectl get command is used to retrieve information about Kubernetes resources. You can use it to get information about nodes, pods, services, deployments, and more. Here's an example of how to get information about all the pods in the default namespace:

```bash
kubectl get pods
```

> This command will return a list of all the pods in the default namespace, along with their status, age, and other details.

### kubectl describe:
The kubectl describe command provides detailed information about a specific Kubernetes resource. For example, you can use it to get information about a specific pod or service. Here's an example of how to describe a pod:

```bash
kubectl describe pod nginx-abc123
```

> This command will return detailed information about the pod with the name nginx-abc123, including its status, IP address, and other details.

### kubectl apply:
The kubectl apply command is used to apply changes to a Kubernetes resource. For example, you can use it to update a deployment or change the configuration of a pod. Here's an example of how to apply a new configuration to a deployment:

```bash
kubectl apply -f nginx-deployment.yaml
```

> This command will apply the configuration in the nginx-deployment.yaml file to the deployment named nginx.

### kubectl delete:
The kubectl delete command is used to delete a Kubernetes resource. You can use it to delete pods, services, deployments, and more. Here's an example of how to delete a deployment:
```bash
kubectl delete deployment nginx
```
> This command will delete the deployment named nginx, along with all the pods associated with it.

### kubectl logs:
The kubectl logs command is used to retrieve logs from a pod. You can use it to view logs for a specific container within a pod, or for the entire pod. Here's an example of how to get the logs for a specific container within a pod:

```bash
kubectl logs mypod -c mycontainer
```

> This command will return the logs for the container named mycontainer within the pod named mypod.

### kubectl exec:
The kubectl exec command is used to execute a command inside a container running in a pod. You can use it to run commands such as bash or sh to interact with the container. Here's an example of how to execute a command inside a container:

```bash
kubectl exec mypod -c mycontainer -- ls
```

> This command will execute the ls command inside the container named mycontainer within the pod named mypod.

kubectl port-forward:
The kubectl port-forward command is used to forward a local port to a port on a pod. You can use it to access services running inside the pod, such as a web application. Here's an example of how to forward port 8080 on your local machine to port 80 on a pod:

```bash
kubectl port-forward pod/mypod 8080:80
```
> This command will forward port 8080 on your local machine to port 80 on the pod named mypod

`kubectl rollout` is a subcommand used to manage rollouts of deployments. A rollout is the process of updating the pods in a deployment to a new version. This is typically done by updating the Docker image used by the deployment.

Here are some examples of how you can use kubectl rollout:

* To view the status of a rollout, you can use the kubectl rollout status command. For example, kubectl rollout status deployment/myapp will show you the status of the myapp deployment.
* To pause a rollout, you can use the kubectl rollout pause command. For example, kubectl rollout pause deployment/myapp will pause the rollout of the myapp deployment.
* To resume a paused rollout, you can use the kubectl rollout resume command. For example, kubectl rollout resume deployment/myapp will resume the rollout of the myapp deployment.
* To undo a rollout and roll back to a previous version, you can use the kubectl rollout undo command. For example, kubectl rollout undo deployment/myapp will roll back the myapp deployment to the previous version.
* To view the history of a rollout, you can use the kubectl rollout history command. For example, kubectl rollout history deployment/myapp will show you the history of the myapp deployment, including the revisions and the changes made in each revision.



* kubectl cluster-info:
This command displays information about the Kubernetes cluster. It provides information about the Kubernetes API server, the Kubernetes version, and the Kubernetes dashboard URL. This command is useful for getting a quick overview of the cluster and its current state.

Example usage:
```
$ kubectl cluster-info
```

Kubernetes master is running at https://kubernetes.example.com
CoreDNS is running at https://kubernetes.example.com/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

* kubectl config:
This command is used to manage Kubernetes configuration files, including contexts, clusters, and users. You can use it to switch between different clusters or contexts. A context is a set of access parameters for a Kubernetes cluster, including the cluster's URL, authentication information, and namespace. The config command can be used to create, modify, or delete context configurations.

Example usage:

```
$ kubectl config view # show the current configuration
$ kubectl config get-contexts # list all available contexts
$ kubectl config use-context prod-cluster # switch to the prod-cluster context
```

* kubectl rollout history:
This command displays the revision history for a deployment, including the date and time of each revision and the reason for the revision. You can use it to view the status of a deployment and roll back to a previous version if needed.

Example usage:

```
$ kubectl rollout history deployment/my-deployment # show the revision history for my-deployment
$ kubectl rollout undo deployment/my-deployment # rollback to the previous revision
```

* kubectl edit:
This command opens a Kubernetes resource in your default editor, allowing you to modify its configuration. You can use it to make quick changes to a resource without having to create a new YAML file. This command is useful for making small changes to resources such as pods or deployments.

Example usage:

```
$ kubectl edit deployment/my-deployment # edit the configuration for my-deployment
```

kubectl label:
This command is used to add or remove labels from Kubernetes resources. Labels are used to categorize resources and make it easier to manage them. You can use labels to organize resources by team, application, or environment.

Example usage:

```
$ kubectl label pod/my-pod env=prod # add the 'env=prod' label to my-pod
$ kubectl label pod/my-pod env- # remove the 'env' label from my-pod
```

* kubectl taint:
This command is used to apply a taint to a node in the Kubernetes cluster. Taints are used to repel pods from nodes, preventing them from running on nodes that don't meet certain requirements. You can use taints to mark nodes as unsuitable for certain workloads, such as workloads that require a lot of CPU or memory.

Example usage:

```
$ kubectl taint nodes my-node key=value:NoSchedule # add the 'key=value' taint to my-node
```

* kubectl annotate:
This command is used to add or modify annotations on Kubernetes resources. Annotations are used to attach arbitrary metadata to resources and can be used to provide additional information about a resource. You can use annotations to store information about a resource that is not part of its core configuration.

Example usage:

```
$ kubectl annotate deployment/my-deployment my-annotation=value # add the 'my-annotation=value' annotation to my-deployment
```

* kubectl exec -it: This command is similar to kubectl exec, but it opens an interactive shell in the container, allowing you to run multiple commands within the container.
* kubectl top: This command displays resource usage statistics for nodes, pods, and containers in the Kubernetes cluster.
* kubectl apply -f: This command is used to apply a Kubernetes resource definition from a YAML or JSON file. You can use it to create, update, or delete resources from the file.

* kubectl config view: This command displays the current Kubernetes configuration. It shows the list of contexts, clusters, and users that are configured on your system.
* kubectl rollout restart: This command restarts a deployment by creating a new revision of the deployment with the same configuration as the current revision. This is useful if you need to apply a configuration change that requires a restart.
* kubectl logs --tail: This command allows you to retrieve the last N lines of logs from a pod. You can use it to view recent log entries without having to retrieve the entire log.
* kubectl rollout undo: This command rolls back a deployment to the previous revision. This is useful if a deployment has a problem that needs to be fixed quickly.
* kubectl exec -p: This command is similar to kubectl exec, but it attaches to the last container that was started in a pod. This is useful if you have a multi-container pod and you want to interact with a specific container.
* kubectl rollout status: This command displays the status of a deployment rollout, including the current revision, the desired revision, and the status of the replica set for each revision.
* kubectl get events: This command displays the recent events in the Kubernetes cluster. It can be useful for troubleshooting issues and identifying problems.
* kubectl apply --dry-run: This command performs a dry run of the kubectl apply command, showing what changes would be made without actually applying them. This is useful for testing changes before applying them to a live environment.
* kubectl top pod: This command displays the CPU and memory usage of a specific pod. You can use it to monitor the resource usage of a pod over time.
* kubectl api-resources: This command displays the available API resources and their short names. It's useful for discovering the Kubernetes resources that are available to you.
* kubectl rollout pause: This command pauses a rollout by scaling down the deployment's replicas to zero. This is useful if you need to temporarily halt a rollout for maintenance or troubleshooting.
* kubectl rollout resume: This command resumes a paused rollout by scaling up the deployment's replicas to the desired count. This is useful if you need to restart a rollout that was paused for maintenance or troubleshooting.
* kubectl explain: This command displays detailed information about a Kubernetes resource, including its fields, their types, and their default values. It's useful for understanding the structure of Kubernetes resources and their configuration options.
* kubectl delete pod --force: This command forcefully deletes a pod without waiting for it to terminate gracefully. This is useful if a pod is stuck in a terminating state and needs to be forcefully deleted.
* kubectl get nodes --show-labels: This command displays the list of nodes in the Kubernetes cluster and their labels. Labels are key-value pairs that can be used to tag nodes with additional metadata.
* kubectl rollout history undo: This command undoes a specific revision of a deployment. This is useful if you need to roll back a deployment to a specific revision rather than the


* kubectl apply --prune: This command applies a configuration change to a Kubernetes resource, but also removes any previously created resources that are no longer specified in the new configuration. This can be useful for cleaning up unused resources.
* kubectl apply --prune -l: This command applies a configuration change to all resources that match a specified label selector, and also removes any previously created resources that are no longer specified in the new configuration. This can be useful for cleaning up unused resources across multiple deployments.
* kubectl get --watch: This command displays real-time updates for a specified Kubernetes resource. It can be useful for monitoring the status of a resource as it changes over time.
* kubectl edit -f -: This command opens the most recently applied configuration for a Kubernetes resource in your default editor. This can be useful for quickly making changes to a resource that was recently applied.


* kubectl create secret: This command creates a new Kubernetes secret. You can use it to store sensitive data like passwords or API keys that your application needs to access.
* kubectl cp: This command allows you to copy files to and from a Kubernetes pod. You can use it to transfer data between your local machine and a running pod.
* kubectl uncordon: This command removes the "unschedulable" taint from a node in a Kubernetes cluster. You can use it to bring a previously marked node back into service.
* kubectl attach: This command attaches to a running container in a Kubernetes pod. You can use it to interact with the container's console or run commands inside the container.
