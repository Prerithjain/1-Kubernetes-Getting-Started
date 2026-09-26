\# Exercise 1 — Hello Pod



\## Kubernetes Hands-On Exercise



This exercise demonstrates how to deploy a simple Nginx web application inside a local Kubernetes cluster using Minikube.



The scenario simulates a lightweight \*\*Zepto storefront and delivery-status application\*\*, represented by the Nginx container image.



\---



\## Objective



The objective of this exercise is to:



\* Set up a local Kubernetes cluster using Minikube.

\* Run an Nginx container as a Kubernetes Pod.

\* Verify that the Pod is running successfully.

\* Expose the Pod using a NodePort Service.

\* Access the application through a web browser.



\---



\## Environment



| Component         | Version / Configuration         |

| ----------------- | ------------------------------- |

| Operating System  | Windows 11 Home Single Language |

| Docker            | 28.3.3                          |

| Minikube          | v1.39.0                         |

| Kubernetes        | v1.37.0                         |

| kubectl           | v1.32.2                         |

| Minikube Driver   | Docker                          |

| Application Image | nginx                           |



\---



\## Business Problem



Imagine working as a DevOps Engineer at \*\*Zepto\*\*.



The product team has developed a lightweight web application that displays the storefront and delivery status for customers.



The application needs to be:



\* Available reliably

\* Portable across environments

\* Easy to deploy

\* Ready for future scaling



For this exercise, the popular \*\*Nginx container image\*\* is used to simulate the application.



\---



\# Step 1 — Start Minikube



Minikube was started using the Docker driver:



```powershell

minikube start --driver=docker

```



The Kubernetes node was then verified:



```powershell

kubectl get nodes

```



Result:



```text

NAME       STATUS   ROLES           AGE     VERSION

minikube   Ready    control-plane   ...     v1.37.0

```



The node reached the `Ready` state successfully.



\---



\# Step 2 — Verify Kubernetes System Pods



The Kubernetes system components were checked using:



```powershell

kubectl get pods -A

```



Core components including CoreDNS, kube-proxy, the API server, controller manager, scheduler, and storage provisioner were running successfully.



\---



\# Step 3 — Create the Nginx Pod



The Nginx application was deployed as a Kubernetes Pod:



```powershell

kubectl run hello-k8s --image=nginx --port=80

```



The Pod was verified using:



```powershell

kubectl get pods

```



Result:



```text

NAME        READY   STATUS    RESTARTS   AGE

hello-k8s   1/1     Running   0          ...

```



The Pod was successfully running with no restarts.



\---



\# Step 4 — Inspect the Pod



Detailed Pod information was obtained using:



```powershell

kubectl get pod hello-k8s -o wide

```



Result:



```text

NAME        READY   STATUS    RESTARTS   AGE   IP           NODE

hello-k8s   1/1     Running   0          ...   10.244.0.3   minikube

```



The Pod received the IP address:



```text

10.244.0.3

```



and was scheduled on the Minikube node.



Additional details were inspected using:



```powershell

kubectl describe pod hello-k8s

```



The events confirmed that Kubernetes:



1\. Scheduled the Pod.

2\. Pulled the Nginx image.

3\. Created the container.

4\. Started the container successfully.



\---



\# Step 5 — Expose the Pod



The Pod was exposed using a NodePort Service:



```powershell

kubectl expose pod hello-k8s --type=NodePort --port=80

```



The Service was verified using:



```powershell

kubectl get services

```



Result:



```text

NAME         TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)

hello-k8s    NodePort   10.104.114.127   <none>        80:32453/TCP

```



The Service maps:



```text

Service Port: 80

NodePort:     32453

```



\---



\# Step 6 — Access the Application



The application was opened using:



```powershell

minikube service hello-k8s

```



Minikube created a local tunnel and opened the service in the default browser.



The Nginx welcome page was displayed successfully.



This confirmed that the application was running inside Kubernetes and accessible through the exposed Service.



\---



\# Kubernetes Resources



The final Kubernetes resources were verified using:



```powershell

kubectl get all

```



Result:



```text

NAME            READY   STATUS    RESTARTS

pod/hello-k8s   1/1     Running   0



NAME                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)

service/hello-k8s    NodePort    10.104.114.127   <none>        80:32453/TCP

service/kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP

```



\---



\# Kubernetes Configuration



The repository also contains declarative Kubernetes configuration files:



\### `pod.yaml`



Defines the Nginx Pod and exposes container port 80.



\### `service.yaml`



Defines a NodePort Service that exposes the Nginx application outside the Pod.



These YAML files document the configuration required to reproduce the deployment.



\---



\# Architecture



```text

&#x20;                 Kubernetes Cluster

&#x20;                        │

&#x20;                   Minikube Node

&#x20;                        │

&#x20;                 ┌──────▼──────┐

&#x20;                 │ hello-k8s   │

&#x20;                 │    Pod      │

&#x20;                 │             │

&#x20;                 │    Nginx    │

&#x20;                 │   Port 80   │

&#x20;                 └──────┬──────┘

&#x20;                        │

&#x20;                        │

&#x20;                 ┌──────▼──────┐

&#x20;                 │ NodePort    │

&#x20;                 │  Service    │

&#x20;                 │             │

&#x20;                 │ 80 → 32453  │

&#x20;                 └──────┬──────┘

&#x20;                        │

&#x20;                        ▼

&#x20;                   Web Browser

&#x20;                 Nginx Welcome Page

```



\---



\# Screenshots



Screenshots demonstrating the exercise are stored in the `screenshots` directory.



\### 1. Kubernetes Cluster Ready



Shows the Minikube node in the `Ready` state.



\### 2. Nginx Pod Running



Shows:



```text

hello-k8s   1/1   Running

```



\### 3. NodePort Service



Shows the `hello-k8s` Service and its NodePort.



\### 4. Nginx Browser Page



Shows the Nginx welcome page served through Kubernetes.



\---



\# What I Learned



Through this exercise, I learned how to:



\* Start a Kubernetes cluster locally using Minikube.

\* Understand the role of a Kubernetes Node.

\* Create a Pod using `kubectl`.

\* Deploy a container image using Kubernetes.

\* Verify Pod status and networking information.

\* Inspect Pod events using `kubectl describe`.

\* Expose a Pod using a NodePort Service.

\* Access a Kubernetes application from a local browser.

\* Understand the basic relationship between Pods, Services, and Nodes.



\---



\# Useful Commands



```powershell

\# Start Minikube

minikube start --driver=docker



\# Check nodes

kubectl get nodes



\# Check all system Pods

kubectl get pods -A



\# Create Pod

kubectl run hello-k8s --image=nginx --port=80



\# Check Pods

kubectl get pods



\# Get detailed Pod information

kubectl get pod hello-k8s -o wide



\# Describe Pod

kubectl describe pod hello-k8s



\# Expose Pod

kubectl expose pod hello-k8s --type=NodePort --port=80



\# Check Services

kubectl get services



\# Check all resources

kubectl get all



\# Open application

minikube service hello-k8s

```



\---



\# Cleanup



After completing the exercise, the Kubernetes resources can be removed with:



```powershell

kubectl delete service hello-k8s

kubectl delete pod hello-k8s

```



The Minikube cluster can be stopped with:



```powershell

minikube stop

```



To completely remove the local Minikube cluster:



```powershell

minikube delete

```



\---



\## Exercise Status



\*\*Exercise 1 — Hello Pod: Completed ✅\*\*



