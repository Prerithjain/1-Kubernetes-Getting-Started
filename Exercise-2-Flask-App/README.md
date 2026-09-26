\# Exercise 2 – Deploying a Flask Application on Kubernetes



\## Objective



Deploy a simple Python Flask application on a local Kubernetes cluster using Minikube and Kubernetes YAML configuration.



This exercise demonstrates:



\- Creating a Flask application

\- Containerizing the application with Docker

\- Building the container image inside Minikube

\- Creating a Kubernetes Deployment

\- Running the Flask application inside a Kubernetes Pod

\- Inspecting the Deployment and Pod

\- Viewing application logs

\- Creating a NodePort Service

\- Accessing the Flask application through Minikube



\---



\## Environment



\- OS: Windows 11

\- Kubernetes: Minikube

\- Kubernetes version: v1.37.0

\- kubectl: v1.32.2

\- Minikube driver: Docker

\- Application: Python Flask

\- Container image: `flask-app:latest`

\- Application port: `15000`



\---



\# 1. Start Minikube



First, the Minikube cluster was started and verified.



```powershell

minikube start --driver=docker

