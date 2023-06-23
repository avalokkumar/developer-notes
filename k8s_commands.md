## k8s Commands

### Resource Management:

#### kubectl create
##### Command: kubectl create
> Explanation: This command is used to create Kubernetes resources. It allows you to specify the type of resource and its configuration.

#### kubectl create deployment:
##### Command: `kubectl create deployment nginx-deployment --image=nginx`
> Explanation: This command creates a deployment named "nginx-deployment" using the "nginx" container image. Deployments manage the lifecycle of pods in Kubernetes.

#### kubectl create deployment with dry-run and YAML output:
##### Command: `kubectl create deployment nginx-deployment --image=nginx --dry-run=client -o yaml`
> Explanation: This command performs a dry run of creating a deployment with the specified image. It generates the YAML representation of the deployment configuration without actually creating it.

#### kubectl create deployment with dry-run, YAML output, and file creation:
##### Command: `kubectl create deployment nginx-deployment --image=nginx --dry-run=client -o yaml > nginx-deployment.yaml`
> Explanation: This command performs a dry run of creating a deployment and saves the resulting YAML configuration to a file named "nginx-deployment.yaml" for later use.

#### kubectl run
##### Command: `kubectl run nginx --image=nginx`
> Explanation: This command creates a pod named "nginx" using the "nginx" container image. Pods are the smallest and simplest unit in the Kubernetes ecosystem.

#### kubectl run with dry-run and YAML output:
##### Command: `kubectl run nginx --image=nginx --dry-run=client -o yaml`
> Explanation: This command performs a dry run of creating a pod with the specified image. It generates the YAML representation of the pod configuration without actually creating it.

#### kubectl run with dry-run, YAML output, and file creation:
##### Command: `kubectl run nginx --image=nginx --dry-run=client -o yaml > nginx-deployment.yaml`
>Explanation: This command performs a dry run of creating a pod and saves the resulting YAML configuration to a file  named "nginx-deployment.yaml" for later use.

#### kubectl expose:
##### Command: `kubectl expose deployment nginx-deployment --port=80 --type=NodePort`
> Explanation: This command creates a service to expose the pods managed by the "nginx-deployment" deployment. The service makes the pods accessible from outside the cluster on a specified port.

#### kubectl expose with dry-run and YAML output:
##### Command: `kubectl expose deployment nginx-deployment --port=80 --type=NodePort --dry-run=client -o yaml`
> Explanation: This command performs a dry run of creating a service for the "nginx-deployment" and generates the YAML representation of the service configuration without actually creating it. 

#### kubectl expose with dry-run, YAML output, and file creation:
##### Command: `kubectl expose deployment nginx-deployment --port=80 --type=NodePort --dry-run=client -o yaml > nginx-service.yaml`
> Explanation: This command performs a dry run of creating a service and saves the resulting YAML configuration to a file named "nginx-service.yaml" for later use.

#### kubectl get

#### kubectl get pods:
##### Command: `kubectl get pods`
> Explanation: This command retrieves information about the pods running in the current namespace. Pods are the smallest and simplest unit in Kubernetes that encapsulates one or more containers.

#### kubectl get pods with wide output:
##### Command: `kubectl get pods -o wide`
> Explanation: This command displays detailed information about the pods, including additional columns such as node name and IP address.

#### kubectl get pods with YAML output:
##### Command: `kubectl get pods -o yaml`
> Explanation: This command retrieves the YAML representation of the pods, including their configuration, and displays it in the output.

#### kubectl get pods with JSON output:
##### Command: `kubectl get pods -o json`
> Explanation: This command retrieves the JSON representation of the pods, including their configuration, and displays it in the output.

#### kubectl get pods with custom columns:
##### Command: `kubectl get pods -o custom-columns=POD_NAME:.metadata.name,POD_STATUS:.status.phase`
> Explanation: This command allows you to define custom columns for the output. In this example, it displays the pod name and its current status (phase).

#### kubectl get pods with JSONPath output (name):
##### Command: `kubectl get pods -o jsonpath='{.items[0].metadata.name}'`
> Explanation: This command uses JSONPath expressions to extract specific information from the pods. In this case, it retrieves the name of the first pod in the list.

#### kubectl get pods with JSONPath output (status):
##### Command: `kubectl get pods -o jsonpath='{.items[0].status.phase}'`
> Explanation: This command retrieves the status phase of the first pod in the list using JSONPath expressions.

#### kubectl get pods with JSONPath output (container image):
##### Command: `kubectl get pods -o jsonpath='{.items[0].spec.containers[0].image}'`
> Explanation: This command retrieves the image of the first container within the first pod in the list using JSONPath expressions.

#### kubectl get pods with JSONPath output (container image, newline):
##### Command: `kubectl get pods -o jsonpath='{.items[0].spec.containers[0].image}{"\n"}'`
> Explanation: This command retrieves the image of the first container within the first pod in the list using JSONPath expressions and adds a newline after the output.

#### kubectl get pods with JSONPath output (multiple container images):
##### Command: `kubectl get pods -o jsonpath='{.items[0:2].spec.containers[0].image}{"\n"}'`
> Explanation: This command retrieves the images of the first two containers within the first two pods in the list using JSONPath expressions and adds a newline after each image.

#### kubectl get pods with JSONPath output (all container images):
##### Command: `kubectl get pods -o jsonpath='{.items[*].spec.containers[0].image}{"\n"}'`
> Explanation: This command retrieves the images of all containers in all pods in the list using JSONPath expressions and adds a newline after each image.

#### kubectl get pods with JSONPath output (range of values - pod names):
##### Command: `kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}'`
> Explanation: This command retrieves the names of all pods in the list using JSONPath expressions and displays them with a newline after each name.

#### kubectl get pods with JSONPath output (range of values - pod names and phases):
##### Command: `kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.phase}{"\n"}{end}'`
> Explanation: This command retrieves the names and phases of all pods in the list using JSONPath expressions and displays them with a tab-separated format.

#### kubectl get pods with JSONPath output (range of values - pod names, phases, and container images):
##### Command: `kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.phase}{"\t"}{.spec.containers[0].image}{"\n"}{end}'`
> Explanation: This command retrieves the names, phases, and container images of all pods in the list using JSONPath expressions and displays them with a tab-separated format.

#### kubectl get pods with JSONPath output (range of values - pod names, phases, and duplicate container images):
##### Command: `kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.phase}{"\t"}{.spec.containers[0].image}{"\t"}{.spec.containers[0].image}{"\n"}{end}'`
> Explanation: This command retrieves the names, phases, and duplicate container images of all pods in the list using JSONPath expressions and displays them with a tab-separated format.

* kubectl describe
  * kubectl describe pod nginx-deployment-5c7588df68-7q8q2
  * kubectl describe pod nginx-deployment-5c7588df68-7q8q2 | grep -i image
  * kubectl describe pod nginx-deployment-5c7588df68-7q8q2 | grep -i image | cut -f2 -d':'
  * kubectl describe pod nginx-deployment-5c7588df68-7q8q2 | grep -i image | cut -f2 -d':' | cut -f1 -d' '
  * kubectl describe pod nginx-deployment-5c7588df68-7q8q2 | grep -i image | cut -f2 -d':' | cut -f1 -d' ' | cut -f2 -d'/'
  * kubectl describe pod nginx-deployment-5c7588df68-7q8q2 | grep -i image | cut -f2 -d':' | cut -f1 -d' ' | cut -f2 -d'/' | cut -f1 -d'@'
  * kubectl describe pod nginx-deployment-5c7588df68-7q8q2 | grep -i image | cut -f2 -d':' | cut -f1 -d' ' | cut -f2 -d'/' | cut -f1 -d'@' | cut -f1 -d'.'
  * kubectl describe pod nginx-deployment-5c7588df68-7q8q2 | grep -i image | cut -f2 -d':' | cut -f1 -d' ' | cut -f2 -d'/' | cut -f1 -d'@' | cut -f1 -d'.' | cut -f1 -d'-'
  * kubectl describe pod nginx-deployment-5c7588df68-7q8q2 | grep -i image | cut -f2 -d':' | cut -f1 -d' ' | cut -f2 -d'/' | cut -f1 -d'@' | cut -f1 -d'.' | cut -f1 -d'-' | cut -f1 -d'_'

* kubectl apply
  * kubectl apply -f nginx-deployment.yaml
  * kubectl apply -f nginx-service.yaml
  * kubectl apply -f nginx-deployment.yaml --record
  * kubectl apply -f nginx-deployment.yaml --record=true
  * kubectl apply -f nginx-deployment.yaml --record=true --record
  * kubectl apply -f nginx-deployment.yaml --record=true --record=true
  * kubectl apply -f nginx-deployment.yaml --record=true --record=true --record

* kubectl delete
  * kubectl delete pod nginx-deployment-5c7588df68-7q8q2
  * kubectl delete pod nginx-deployment-5c7588df68-7q8q2 --grace-period=0 --force
  * kubectl delete pod nginx-deployment-5c7588df68-7q8q2 --grace-period=0 --force=true
  
* kubectl logs
  * kubectl logs nginx-deployment-5c7588df68-7q8q2
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true --timestamps
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true --timestamps=true
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true --timestamps=true --since=1h
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z"
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --container=nginx
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --container=nginx --previous
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --container=nginx --previous=true
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --container=nginx --previous=true --limit-bytes=1024
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --container=nginx --previous=true --limit-bytes=1024 --limit-logs=10
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --container=nginx --previous=true --limit-bytes=1024 --limit-logs=10 --ignore-errors=true
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --container=nginx --previous=true --limit-bytes=1024 --limit-logs=10 --ignore-errors=true --pod-running-timeout=1h
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10 --follow
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10 --follow=true
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10 --follow=true --timestamps
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10 --follow=true --timestamps=true
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10 --follow=true --timestamps=true --since=1h
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z"
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --previous
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --previous=true
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --previous=true --limit-bytes=1024
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --previous=true --limit-bytes=1024 --limit-logs=10
  * kubectl logs nginx-deployment-5c7588df68-7q8q2 --all-containers=true --tail=10 --follow=true --timestamps=true --since=1h --since-time="2020-01-01T00:00:00Z" --previous=true --limit-bytes=1024 --limit-logs=10 --ignore-errors=true

* kubectl exec
  * kubectl exec nginx-deployment-5c7588df68-7q8q2 -- ls -l
  * kubectl exec nginx-deployment-5c7588df68-7q8q2 -- ls -l /usr/share/nginx/html
  * kubectl exec nginx-deployment-5c7588df68-7q8q2 -- ls -l /usr/share/nginx/html/index.html
  * kubectl exec nginx-deployment-5c7588df68-7q8q2 -- cat /usr/share/nginx/html/index.html
  * kubectl exec nginx-deployment-5c7588df68-7q8q2 -- cat /usr/share/nginx/html/index.html | grep nginx
  * kubectl exec nginx-deployment-5c7588df68-7q8q2 -- bin/bash
  * kubectl exec nginx-deployment-5c7588df68-7q8q2 -- bin/bash -c "ls -l /usr/share/nginx/html"
  * kubectl exec -it nginx-deployment-5c7588df68-7q8q2 -- bin/bash
  * kubectl exec -it nginx-deployment-5c7588df68-7q8q2 -- bin/bash -c "ls -l /usr/share/nginx/html"
  * kubectl exec -it nginx-deployment-5c7588df68-7q8q2 -- bin/bash -c "ls -l /usr/share/nginx/html" -- /bin/sh
  * kubectl exec -it nginx-deployment-5c7588df68-7q8q2 -- bin/bash -c "ls -l /usr/share/nginx/html" -- /bin/sh -c "ls -l /usr/share/nginx/html"

* kubectl port-forward
  * kubectl port-forward nginx-deployment-5c7588df68-7q8q2 8080:80
  * kubectl port-forward nginx-deployment-5c7588df68-7q8q2 8080:80 --address

* kubectl rollout
  * kubectl rollout history
  * kubectl rollout history deployment nginx-deployment
  * kubectl rollout history deployment nginx-deployment --revision=2
  * kubectl rollout history deployment nginx-deployment --revision=2 --record
  * kubectl rollout undo
  * kubectl rollout undo deployment nginx-deployment
  * kubectl rollout undo deployment nginx-deployment --to-revision=2
  * kubectl rollout undo deployment nginx-deployment --to-revision=2 --record
  * kubectl rollout restart
  * kubectl rollout restart deployment nginx-deployment
  * kubectl rollout restart deployment nginx-deployment --record
  * kubectl rollout status
  * kubectl rollout status deployment nginx-deployment
  * kubectl rollout status deployment nginx-deployment --timeout=1m
  * kubectl rollout status deployment nginx-deployment --timeout=1m --watch=false
  * kubectl rollout pause
  * kubectl rollout pause deployment nginx-deployment
  * kubectl rollout resume
  * kubectl rollout resume deployment nginx-deployment
  
* kubectl scale
  * kubectl scale --replicas=3 deployment nginx-deployment
  * kubectl scale --replicas=3 replicaset nginx-deployment-5c7588df68
  * kubectl scale --replicas=3 statefulset web
  * kubectl scale --replicas=3 daemonset my-daemonset
  * kubectl scale --replicas=3 job my-job
  * kubectl scale --replicas=3 cronjob my-cronjob
  * kubectl scale --replicas=3 deployment nginx-deployment --current-replicas=2
  * kubectl scale --replicas=3 deployment nginx-deployment --current-replicas=2 --resource-version=1542

    
### Configuration Management:

* kubectl cluster-info
  * kubectl cluster-info dump
  * kubectl cluster-info dump --output-directory=/tmp/cluster-info
  * kubectl cluster-info dump --output-directory=/tmp/cluster-info --namespaces=default
  * kubectl cluster-info dump --output-directory=/tmp/cluster-info --namespaces=default --all-namespaces
  * kubectl cluster-info dump --output-directory=/tmp/cluster-info --namespaces=default --all-namespaces --output-version=v1
  * kubectl cluster-info dump --output-directory=/tmp/cluster-info --namespaces=default --all-namespaces --output-version=v1 --log-file=/tmp/cluster-info.log
  * kubectl cluster-info dump --output-directory=/tmp/cluster-info --namespaces=default --all-namespaces --output-version=v1 --log-file=/tmp/cluster-info.log --log-file-max-size=10
  * kubectl cluster-info dump --output-directory=/tmp/cluster-info --namespaces=default --all-namespaces --output-version=v1 --log-file=/tmp/cluster-info.log --log-file-max-size=10 --log-file-max-num=5
  * kubectl cluster-info dump --output-directory=/tmp/cluster-info --namespaces=default --all-namespaces --output-version=v1 --log-file=/tmp/cluster-info.log --log-file-max-size=10 --log-file-max-num=5 --image-file=/tmp/cluster-info.tar.gz

* kubectl config
  * kubectl config view
  * kubectl config view --minify
  * kubectl config view --minify --flatten
  * kubectl config view --minify --flatten --output=json
  * kubectl config view --minify --flatten --output=yaml
  * kubectl config view --minify --flatten --output=jsonpath='{.clusters[0].cluster.server}'
  * kubectl config view --minify --flatten --output=jsonpath='{.clusters[0].cluster.server}' --raw
  * kubectl config view --minify --flatten --output=jsonpath='{.clusters[0].cluster.server}' --raw --log-file=/tmp/kubectl.log

* kubectl config current-context
  * kubectl config current-context --log-file=/tmp/kubectl.log
  * kubectl config current-context --raw
  * kubectl config current-context --raw --log-file=/tmp/kubectl.log
  * kubectl config current-context --output=json
  * kubectl config current-context --output=json --log-file=/tmp/kubectl.log
* kubectl config use-context
  * kubectl config use-context kubernetes-admin@kubernetes
  * kubectl config use-context kubernetes-admin@kubernetes --log-file=/tmp/kubectl.log
  * kubectl config use-context kubernetes-admin@kubernetes --raw
  * kubectl config use-context kubernetes-admin@kubernetes --raw --log-file=/tmp/kubectl.log
  * kubectl config use-context kubernetes-admin@kubernetes --output=json
  * kubectl config use-context kubernetes-admin@kubernetes --output=json --log-file=/tmp/kubectl.log
* kubectl config set-cluster
  * kubectl config set-cluster kubernetes --server=https://
  * kubectl config set-cluster kubernetes --server=https:// --log-file=/tmp/kubectl.log
* kubectl config set-credentials
  * kubectl config set-credentials kubernetes-admin --username=admin --password=123456
  * kubectl config set-credentials kubernetes-admin --username=admin --password=123456 --log-file=/tmp/kubectl.log
* kubectl config set-context
  * kubectl config set-context kubernetes-admin@kubernetes --cluster=kubernetes --user=kubernetes-admin
  * kubectl config set-context kubernetes-admin@kubernetes --cluster=kubernetes --user=kubernetes-admin --log-file=/tmp/kubectl.log
* kubectl config unset
  * kubectl config unset users.kubernetes-admin
  * kubectl config unset users.kubernetes-admin --log-file=/tmp/kubectl.log
* kubectl config rename-context
  * kubectl config rename-context kubernetes-admin@kubernetes kubernetes-admin@kubernetes
  * kubectl config rename-context kubernetes-admin@kubernetes kubernetes-admin@kubernetes --log-file=/tmp/kubectl.log
* kubectl rollout history
  * kubectl rollout history deployment nginx-deployment
  * kubectl rollout history deployment nginx-deployment --revision=1
  * kubectl rollout history deployment nginx-deployment --revision=1 --output=json
  * kubectl rollout history deployment nginx-deployment --revision=1 --output=json --log-file=/tmp/kubectl.log
  * kubectl rollout history deployment nginx-deployment --revision=1 --output=json --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl rollout history deployment nginx-deployment --revision=1 --output=json --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
* kubectl rollout pause
  * kubectl rollout pause deployment nginx-deployment
  * kubectl rollout pause deployment nginx-deployment --log-file=/tmp/kubectl.log
* kubectl rollout resume
  * kubectl rollout resume deployment nginx-deployment
  * kubectl rollout resume deployment nginx-deployment --log-file=/tmp/kubectl.log
* kubectl rollout undo
  * kubectl rollout undo deployment nginx-deployment
  * kubectl rollout undo deployment nginx-deployment --log-file=/tmp/kubectl.log
  * kubectl rollout undo deployment nginx-deployment --to-revision=1
  * kubectl rollout undo deployment nginx-deployment --to-revision=1 --log-file=/tmp/kubectl.log
* kubectl rollout restart
  * kubectl rollout restart deployment nginx-deployment
  * kubectl rollout restart deployment nginx-deployment --log-file=/tmp/kubectl.log
* kubectl edit
  * kubectl edit deployment nginx-deployment
  * kubectl edit deployment nginx-deployment --log-file=/tmp/kubectl.log
  * kubectl edit deployment nginx-deployment --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl edit deployment nginx-deployment --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
  * kubectl edit deployment nginx-deployment --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5 --log-file-max-backups=5
* kubectl label
  * kubectl label deployment nginx-deployment app=nginx
  * kubectl label deployment nginx-deployment app=nginx --log-file=/tmp/kubectl.log
  * kubectl label deployment nginx-deployment app=nginx --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl label deployment nginx-deployment app=nginx --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
  * kubectl label deployment nginx-deployment app=nginx --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5 --log-file-max-backups=5
  * kubectl label deployment nginx-deployment app=nginx --overwrite
  * kubectl label deployment nginx-deployment app=nginx --overwrite --log-file=/tmp/kubectl.log
  * kubectl label deployment nginx-deployment app=nginx --overwrite --log-file=/tmp/kubectl.log --log-file-max-size=10
* kubectl annotate
  * kubectl annotate deployment nginx-deployment app=nginx
  * kubectl annotate deployment nginx-deployment app=nginx --log-file=/tmp/kubectl.log
  * kubectl annotate deployment nginx-deployment app=nginx --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl annotate deployment nginx-deployment app=nginx --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
  * kubectl annotate deployment nginx-deployment app=nginx --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5 --log-file-max-backups=5
  * kubectl annotate deployment nginx-deployment app=nginx --overwrite
  * kubectl annotate deployment nginx-deployment app=nginx --overwrite --log-file=/tmp/kubectl.log
  * kubectl annotate deployment nginx-deployment app=nginx --overwrite --log-file=/tmp/kubectl.log --log-file-max-size=10
* kubectl rollout status
  * kubectl rollout status deployment nginx-deployment
  * kubectl rollout status deployment nginx-deployment --log-file=/tmp/kubectl.log
  * kubectl rollout status deployment nginx-deployment --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl rollout status deployment nginx-deployment --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
  * kubectl rollout status deployment nginx-deployment --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5 --log-file-max-backups=5
* kubectl taint
  * kubectl taint node node1 key=value:NoSchedule
  * kubectl taint node node1 key=value:NoSchedule --log-file=/tmp/kubectl.log
  * kubectl taint node node1 key=value:NoSchedule --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl taint node node1 key=value:NoSchedule --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
  * kubectl taint node node1 key=value:NoSchedule --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5 --log-file-max-backups=5
  * kubectl taint node node1 key=value:NoSchedule --overwrite
  * kubectl taint node node1 key=value:NoSchedule --overwrite --log-file=/tmp/kubectl.log
  * kubectl taint node node1 key=value:NoSchedule --overwrite --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl taint node node1 key=value:NoSchedule --overwrite --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
* kubectl top
  * kubectl top node
  * kubectl top node --log-file=/tmp/kubectl.log
  * kubectl top node --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl top node --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
  * kubectl top node --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5 --log-file-max-backups=5
  * kubectl top pod
  * kubectl top pod --log-file=/tmp/kubectl.log
  * kubectl top pod --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl top pod --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
  * kubectl top pod --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5 --log-file-max-backups=5
* kubectl logs
  * kubectl logs pod/nginx
  * kubectl logs pod/nginx --log-file=/tmp/kubectl.log
  * kubectl logs pod/nginx --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl logs pod/nginx --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
  * kubectl logs pod/nginx --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5 --log-file-max-backups=5
  * kubectl logs pod/nginx --tail=10
  * kubectl logs pod/nginx --tail=10 --log-file=/tmp/kubectl.log
  * kubectl logs pod/nginx --tail=10 --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl logs pod/nginx --tail=10 --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
  * kubectl logs pod/nginx --tail=10 --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5 --log-file-max-backups=5
  * kubectl logs pod/nginx --tail=10 --follow
  * kubectl logs pod/nginx --tail=10 --follow --log-file=/tmp/kubectl.log
  * kubectl logs pod/nginx --tail=10 --follow --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl logs pod/nginx --tail=10 --follow --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5
  * kubectl logs pod/nginx --tail=10 --follow --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5 --log-file-max-backups=5


* kubectl apply -f
  * kubectl apply -f pod.yaml
  * kubectl apply -f pod.yaml --log-file=/tmp/kubectl.log
  * kubectl apply -f pod.yaml --log-file=/tmp/kubectl.log --log-file-max-size=10
  * kubectl apply -f pod.yaml --log-file=/tmp/kubectl.log --log-file-max-size=10 --log-file-max-num=5

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
* kubectl api-versions
* kubectl api-versions -o json
* kubectl api-versions -o yaml
* kubectl api-versions -o wide
* kubectl api-versions -o custom-columns=NAME:.name,VERSION:.version
* kubectl api-versions -o custom-columns=NAME:.name,VERSION:.version --sort-by .name
* kubectl api-versions -o custom-columns=NAME:.name,VERSION:.version --sort-by .version
* kubectl api-versions -o custom-columns=NAME:.name,VERSION:.version --sort-by .version --reverse
* kubectl api-versions -o custom-columns=NAME:.name,VERSION:.version --sort-by .version --reverse --no-headers
* kubectl api-versions -o custom-columns=NAME:.name,VERSION:.version --sort-by .version --reverse --no-headers | head -n 1
* kubectl api-versions -o custom-columns=NAME:.name,VERSION:.version --sort-by .version --reverse --no-headers | tail -n 1
* kubectl api-versions -o custom-columns=NAME:.name,VERSION:.version --sort-by .version --reverse --no-headers | grep v1

### Rollout Management:

* kubectl rollout pause
* kubectl rollout resume

### Resource Deletion:

* kubectl delete pod --force

### Resource Configuration:

* kubectl explain

---
******
---
### kubectl create:


The kubectl create command is used to create new Kubernetes resources. For example, you can create a new deployment, service, or pod using this command. Here's an example of how to create a new deployment:
```bash
kubectl create deployment nginx --image=nginx
```

> This command creates a new deployment named nginx using the official nginx Docker image. You can then use the kubectl get command to see the status of the deployment.

---
### kubectl get:
The kubectl get command is used to retrieve information about Kubernetes resources. You can use it to get information about nodes, pods, services, deployments, and more. Here's an example of how to get information about all the pods in the default namespace:

```bash
kubectl get pods
```

> This command will return a list of all the pods in the default namespace, along with their status, age, and other details.
---
### kubectl describe:
The kubectl describe command provides detailed information about a specific Kubernetes resource. For example, you can use it to get information about a specific pod or service. Here's an example of how to describe a pod:

```bash
kubectl describe pod nginx-abc123
```

> This command will return detailed information about the pod with the name nginx-abc123, including its status, IP address, and other details.
---
### kubectl apply:
The kubectl apply command is used to apply changes to a Kubernetes resource. For example, you can use it to update a deployment or change the configuration of a pod. Here's an example of how to apply a new configuration to a deployment:

```bash
kubectl apply -f nginx-deployment.yaml
```

> This command will apply the configuration in the nginx-deployment.yaml file to the deployment named nginx.
---
### kubectl delete:
The kubectl delete command is used to delete a Kubernetes resource. You can use it to delete pods, services, deployments, and more. Here's an example of how to delete a deployment:
```bash
kubectl delete deployment nginx
```
> This command will delete the deployment named nginx, along with all the pods associated with it.
---
### kubectl logs:
The kubectl logs command is used to retrieve logs from a pod. You can use it to view logs for a specific container within a pod, or for the entire pod. Here's an example of how to get the logs for a specific container within a pod:

```bash
kubectl logs mypod -c mycontainer
```

> This command will return the logs for the container named mycontainer within the pod named mypod.
---
### kubectl exec:
The kubectl exec command is used to execute a command inside a container running in a pod. You can use it to run commands such as bash or sh to interact with the container. Here's an example of how to execute a command inside a container:

```bash
kubectl exec mypod -c mycontainer -- ls
```

> This command will execute the ls command inside the container named mycontainer within the pod named mypod.
---
### kubectl port-forward:
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


---
### kubectl cluster-info:
This command displays information about the Kubernetes cluster. It provides information about the Kubernetes API server, the Kubernetes version, and the Kubernetes dashboard URL. This command is useful for getting a quick overview of the cluster and its current state.

Example usage:
```
$ kubectl cluster-info
```

> Kubernetes master is running at https://kubernetes.example.com
> CoreDNS is running at https://kubernetes.example.com/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
---
###  kubectl config:
This command is used to manage Kubernetes configuration files, including contexts, clusters, and users. You can use it to switch between different clusters or contexts. A context is a set of access parameters for a Kubernetes cluster, including the cluster's URL, authentication information, and namespace. The config command can be used to create, modify, or delete context configurations.

Example usage:

```
$ kubectl config view # show the current configuration
$ kubectl config get-contexts # list all available contexts
$ kubectl config use-context prod-cluster # switch to the prod-cluster context
```
---
###  kubectl rollout history:
This command displays the revision history for a deployment, including the date and time of each revision and the reason for the revision. You can use it to view the status of a deployment and roll back to a previous version if needed.

Example usage:

```
$ kubectl rollout history deployment/my-deployment # show the revision history for my-deployment
$ kubectl rollout undo deployment/my-deployment # rollback to the previous revision
```
---
###  kubectl edit:
This command opens a Kubernetes resource in your default editor, allowing you to modify its configuration. You can use it to make quick changes to a resource without having to create a new YAML file. This command is useful for making small changes to resources such as pods or deployments.

Example usage:

```
$ kubectl edit deployment/my-deployment # edit the configuration for my-deployment
```
---
### kubectl label:
This command is used to add or remove labels from Kubernetes resources. Labels are used to categorize resources and make it easier to manage them. You can use labels to organize resources by team, application, or environment.

Example usage:

```
$ kubectl label pod/my-pod env=prod # add the 'env=prod' label to my-pod
$ kubectl label pod/my-pod env- # remove the 'env' label from my-pod
```
---
###  kubectl taint:
This command is used to apply a taint to a node in the Kubernetes cluster. Taints are used to repel pods from nodes, preventing them from running on nodes that don't meet certain requirements. You can use taints to mark nodes as unsuitable for certain workloads, such as workloads that require a lot of CPU or memory.

Example usage:

```
$ kubectl taint nodes my-node key=value:NoSchedule # add the 'key=value' taint to my-node
```
---
###  kubectl annotate:
This command is used to add or modify annotations on Kubernetes resources. Annotations are used to attach arbitrary metadata to resources and can be used to provide additional information about a resource. You can use annotations to store information about a resource that is not part of its core configuration.

Example usage:

```
$ kubectl annotate deployment/my-deployment my-annotation=value # add the 'my-annotation=value' annotation to my-deployment
```
---
###  kubectl exec -it:

The kubectl exec -it command allows you to run an interactive shell session in a container running in a pod. This allows you to execute commands within the container and troubleshoot issues.

Example:

```
kubectl exec -it my-pod -- /bin/bash
```
> This command starts an interactive shell session within the container running in the my-pod pod.

---
###  kubectl top:
The kubectl top command allows you to view resource usage statistics for nodes, pods, and containers in the Kubernetes cluster.

Example:
```
kubectl top nodes
```
> This command displays resource usage statistics for all the nodes in the Kubernetes cluster.

```
kubectl top pods
```
This command displays resource usage statistics for all the pods in the Kubernetes cluster.

```
kubectl top pods --containers
```
> This command displays resource usage statistics for all the containers in all the pods in the Kubernetes cluster.

---
###  kubectl apply -f:
The kubectl apply -f command is used to apply a Kubernetes resource definition from a YAML or JSON file. This can be used to create, update, or delete resources from the file.

Example:
```
kubectl apply -f my-deployment.yaml
```
This command applies the Kubernetes deployment configuration defined in the my-deployment.yaml file.
---
###  kubectl config view:
The kubectl config view command displays the current Kubernetes configuration. It shows the list of contexts, clusters, and users that are configured on your system.

Example:
```
kubectl config view
```
> This command displays the current Kubernetes configuration on your system.
---
###  kubectl rollout restart:
The kubectl rollout restart command restarts a deployment by creating a new revision of the deployment with the same configuration as the current revision. This is useful if you need to apply a configuration change that requires a restart.

Example:
```
kubectl rollout restart deployment/my-deployment
```

> This command restarts the deployment named my-deployment by creating a new revision with the same configuration as the current revision.

---
###  kubectl logs --tail:
The kubectl logs --tail command allows you to retrieve the last N lines of logs from a pod. This is useful for troubleshooting issues in pods and viewing recent log entries without having to retrieve the entire log.

Example:
```
kubectl logs my-pod --tail=10
```
> This command retrieves the last 10 lines of logs from the my-pod pod.
---
###  kubectl rollout undo:
The kubectl rollout undo command rolls back a deployment to the previous revision. This is useful if a deployment has a problem that needs to be fixed quickly.

Example:
```
kubectl rollout undo deployment/my-deployment
```
> This command rolls back the deployment named my-deployment to the previous revision.
---
###  kubectl exec -p:
The kubectl exec -p command is similar to kubectl exec, but it attaches to the last container that was started in a pod. This is useful if you have a multi-container pod and you want to interact with a specific container.

Example:
```
kubectl exec -p my-pod my-container -- /bin/bash
```
> This command attaches to the last container that was started in the my-pod pod and starts an interactive shell session within the my-container container.

---
###  kubectl rollout status:
The kubectl rollout status command displays the status of a deployment rollout, including the current revision, the desired revision, and the status of the replica set for each revision.

Example:
```
kubectl rollout status deployment/my-deployment
```
> This command displays the rollout status of the deployment named my-deployment.
---
###  kubectl get events:
The kubectl get events command displays the recent events in the Kubernetes cluster. It can be useful for troubleshooting issues and identifying problems.

Example:
```
kubectl get events
```
> This command displays the recent events in the Kubernetes cluster.
---
###  kubectl apply --dry-run:
The kubectl apply --dry-run command performs a dry run of the kubectl apply command, showing what changes would be made without actually applying them. This is useful for testing changes before applying them to a live environment.

Example:
```
kubectl apply --dry-run -f my-deployment.yaml
```
> This command performs a dry run of the kubectl apply command using the Kubernetes deployment configuration defined in the my-deployment.yaml file.
---
### kubectl top pod: 
This command is used to monitor the resource usage of a specific pod in a Kubernetes cluster. It displays the CPU and memory usage of a pod over time. For example, the following command displays the resource usage of the pod named my-pod in the my-namespace namespace:

```
kubectl top pod my-pod -n my-namespace
````

### kubectl api-resources: 
This command displays the available API resources and their short names in a Kubernetes cluster. It's useful for discovering the Kubernetes resources that are available to you. For example, the following command lists all the available API resources:

```
kubectl api-resources
```

### kubectl rollout pause: 
This command pauses a rollout by scaling down the deployment's replicas to zero. It's useful if you need to temporarily halt a rollout for maintenance or troubleshooting. For example, the following command pauses the rollout of the deployment named my-deployment:

```
kubectl rollout pause deployment/my-deployment
```
---
### kubectl rollout resume: 
This command resumes a paused rollout by scaling up the deployment's replicas to the desired count. It's useful if you need to restart a rollout that was paused for maintenance or troubleshooting. For example, the following command resumes the rollout of the deployment named my-deployment:

```
kubectl rollout resume deployment/my-deployment
```
---
### kubectl explain: 
This command displays detailed information about a Kubernetes resource, including its fields, their types, and their default values. It's useful for understanding the structure of Kubernetes resources and their configuration options. For example, the following command displays the detailed information about the Pod resource:

```
kubectl explain pod
```
---
### kubectl delete pod --force: 
This command forcefully deletes a pod without waiting for it to terminate gracefully. It's useful if a pod is stuck in a terminating state and needs to be forcefully deleted. For example, the following command forcefully deletes the pod named my-pod:

```
kubectl delete pod my-pod --force
```
---
### kubectl get nodes --show-labels: 
This command displays the list of nodes in the Kubernetes cluster and their labels. Labels are key-value pairs that can be used to tag nodes with additional metadata. For example, the following command lists all the nodes in the cluster along with their labels:

```
kubectl get nodes --show-labels
```

---
### kubectl rollout history undo: 
This command undoes a specific revision of a deployment. It's useful if you need to roll back a deployment to a specific revision rather than the most recent one. For example, the following command rolls back the deployment named my-deployment to the revision number 2:

```
kubectl rollout undo deployment/my-deployment --to-revision=2
```
---

### kubectl apply --prune:
This command applies a configuration change to a Kubernetes resource and also removes any previously created resources that are no longer specified in the new configuration. This helps in cleaning up unused resources. For example, to apply a configuration change to a deployment and remove any previously created resources that are no longer specified in the new configuration, use the following command:
```
kubectl apply --prune -f deployment.yaml
```
This will apply the changes to the deployment specified in deployment.yaml file and remove any previously created resources that are no longer specified in the new configuration.

### kubectl apply --prune -l:
This command applies a configuration change to all resources that match a specified label selector and also removes any previously created resources that are no longer specified in the new configuration. For example, to apply a configuration change to all resources with the label app=nginx and remove any previously created resources that are no longer specified in the new configuration, use the following command:

```
kubectl apply --prune -l app=nginx -f nginx.yaml
```
This will apply the changes to all resources with the label app=nginx specified in nginx.yaml file and remove any previously created resources that are no longer specified in the new configuration.

### kubectl get --watch:
This command displays real-time updates for a specified Kubernetes resource. This is useful for monitoring the status of a resource as it changes over time. For example, to monitor the pods in the default namespace, use the following command:

```
kubectl get pods --watch
```
This will display real-time updates for all the pods in the default namespace.

### kubectl edit -f -:
This command opens the most recently applied configuration for a Kubernetes resource in your default editor. This is useful for quickly making changes to a resource that was recently applied. For example, to edit the configuration of the most recently applied deployment, use the following command:

```
kubectl edit -f deployment.yaml
```
This will open the most recently applied configuration for the deployment specified in deployment.yaml file in your default editor.

### kubectl create secret:
This command creates a new Kubernetes secret that can be used to store sensitive data like passwords or API keys that your application needs to access. For example, to create a secret that contains a password, use the following command:

```
kubectl create secret generic mysecret --from-literal=password=mypassword
```
This will create a new secret named mysecret that contains a key-value pair where the key is password and the value is mypassword.

### kubectl cp:
This command allows you to copy files to and from a Kubernetes pod. This is useful for transferring data between your local machine and a running pod. For example, to copy a file named myfile.txt from a pod named mypod in the default namespace to your local machine, use the following command:

```
kubectl cp default/mypod:/path/to/myfile.txt ./myfile.txt
```

This will copy the file named myfile.txt from the pod named mypod in the default namespace to your local machine.

### kubectl uncordon:
This command removes the "unschedulable" taint from a node in a Kubernetes cluster. This is useful for bringing a previously marked node back into service. For example, to remove the unschedulable taint from a node named mynode, use the following command:

```
kubectl uncordon mynode
```

This will remove the unschedulable taint from the node named mynode.

###  kubectl attach: 
This command attaches to a running container in a Kubernetes pod. You can use it to interact with the container's console or run commands inside the container.
Example:

Suppose you have a pod named "nginx" running a container named "nginx-container". You can attach to the container's console using the following command:

```
kubectl attach nginx -c nginx-container
```
This will attach your terminal to the console of the nginx-container in the nginx pod. From there, you can interact with the container's shell or run commands inside the container.

If the container is running multiple processes, you can specify which process to attach to using the --process flag. For example, if the container is running both an nginx web server and a shell, you can attach to the shell using the following command:

```
kubectl attach nginx -c nginx-container --process sh
```

This will attach your terminal to the shell process inside the nginx-container. You can then interact with the shell as if you were logged into the container.
