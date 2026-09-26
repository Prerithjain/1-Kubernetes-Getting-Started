# Exercise 1 — Hello Pod

## Kubernetes Hands-On Exercise

This exercise demonstrates how to deploy a simple Nginx web application inside a local Kubernetes cluster using Minikube.

The scenario simulates a lightweight **Zepto storefront and delivery-status application**, represented by the Nginx container image.

---

## Objective

The objective of this exercise is to:

- Set up a local Kubernetes cluster using Minikube.
- Run an Nginx container as a Kubernetes Pod.
- Verify that the Pod is running successfully.
- Expose the Pod using a NodePort Service.
- Access the application through a web browser.

---

## Environment

| Component | Version / Configuration |
|---|---|
| Operating System | Windows 11 Home Single Language |
| Docker | 28.3.3 |
| Minikube | v1.39.0 |
| Kubernetes | v1.37.0 |
| kubectl | v1.32.2 |
| Minikube Driver | Docker |
| Application Image | nginx |

---

## Business Problem

Imagine working as a DevOps Engineer at **Zepto**.

The product team has developed a lightweight web application that displays the storefront and delivery status for customers.

The application needs to be:

- Available reliably
- Portable across environments
- Easy to deploy
- Ready for future scaling

For this exercise, the popular **Nginx container image** is used to simulate the application.

---

# Step 1 — Start Minikube

Minikube was started using the Docker driver:

```powershell
minikube start --driver=docker
