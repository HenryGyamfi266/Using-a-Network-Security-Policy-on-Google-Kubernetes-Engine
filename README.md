# Using-a-Network-Security-Policy-on-Google-Kubernetes-Engine

## Overview
This lab guides you through improving security in Google Kubernetes Engine (GKE) by enforcing the Principle of Least Privilege, which limits access to only necessary resources.
Security is implemented at two levels: (1) Firewall Rules at the VPC level, which control network-wide access, and (2) Kubernetes Network Policies, 
which provide finer control over pod-to-pod communication within the cluster.

In this project, I set up a private GKE cluster and a bastion host, providing a secure entry point for cluster access. 
Within this setup, a simple HTTP server and two client pods will be provisioned. I will create Network Policies to restrict access, allowing only one of the client pods to connect to the server.
This approach minimizes exposure by isolating critical resources and securing intra-cluster communications. 
The project is part of Google Kubernetes Engine Helmsman’s resources, designed to give hands-on experience in implementing Binary Authorization and network security in Kubernetes.

## Architecture of Project
In this architecture, a private, standard mode Kubernetes cluster with Dataplane V2 (where network policies are enabled by default) is configured for enhanced security. 
As the cluster is private, neither the API nor worker nodes are accessible from the internet. To manage access, a bastion host is set up with a firewall rule, 
designating its IP as an authorized network, which permits it to access the API.

Within the cluster, three workloads are provisioned:
hello-server: a simple HTTP server with an internally accessible endpoint.
hello-client-allowed: a pod configured to access hello-server and labeled to allow network policy-based connection.
hello-client-blocked: a similar pod but labeled such that the Network Policy restricts it from connecting to hello-server.
This setup demonstrates granular access control within GKE using private cluster configurations, authorized networks, and Network Policies for secure intra-cluster communication






