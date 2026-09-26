\# Exercise 3 — Scaling Flask App with ReplicaSet



\## Objective



Deploy a Flask-based Flash Sale application on a single-node Kubernetes cluster using a ReplicaSet.



This exercise demonstrates:



\- ReplicaSets and Pods

\- Scaling a Flask application

\- Kubernetes self-healing

\- Readiness and liveness probes

\- Service-based access to Pods

\- Pod distribution across a single node



\---



\## Real-Life Tech Use Case — E-commerce Flash Sale



During an e-commerce flash sale, application traffic can increase significantly.



Instead of running a single Pod, Kubernetes can run multiple identical Pods containing the same application. A ReplicaSet maintains the desired number of Pods and automatically replaces a Pod if it fails.



In this exercise:



```text

3 replicas → 5 replicas → delete 1 Pod → automatic replacement

