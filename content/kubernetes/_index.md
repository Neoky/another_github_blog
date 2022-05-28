+++
title = "Kubernetes"
date = 2021-11-14T17:38:23-06:00
weight = 5
chapter = true
pre = "<b>X. </b>"
+++

### Kubernetes

# Where to start?

Tools? Self-managed? Hosted? 

* Beginner Cookbook
Create simplified opener to kubernetes essentials.
https://aveuiller.github.io/kubernetes_apprentice_cookbook.html

# Tools

## IDE

* Monokle
https://github.com/kubeshop/monokle

## Services

* external-secrets
https://github.com/external-secrets/kubernetes-external-secrets

* PostgreSQL 14
How to get pg14 on k8s with examples.
https://blog.crunchydata.com/blog/postgresql-14-on-kubernetes

* Kubecost
Good tool for estimating how much each pod is costing your. This blog shows how to use it with labels. This is good if you are hosting multiple clients.
https://blog.kubecost.com/blog/kubernetes-labels/

* Goldilocks
Service built upon Vertical Pod Autoscaler. Instead of stopping and restarting pops based on resources this service provides a dashboard view to recommendations.
https://goldilocks.docs.fairwinds.com/installation/#installation-2


## Ingress controllers

* Ambassador / Emissary-Ingress
Install with Helm
https://www.getambassador.io/docs/emissary/latest/topics/install/helm/
Used this to actually get emissary-ingress working. The trick was putting in the listener from edge.
https://www.getambassador.io/docs/emissary/latest/tutorials/getting-started/

## CLI Tools
* Krew
* Kubectx 
* Kube-ps1
* Kail
* K9s

* Silver Surfer
Tool to help upgrade kubernetes objects between versions by devtron-labs.
https://github.com/devtron-labs/silver-surfer

* Kubescape
Tool for testing if Kubernetes is deployed securely.
https://github.com/armosec/kubescape#readme

* jsonl-graph
by Nikolaydubina, transforms kubectl json outputs into incredible graphs to view k8s resources.
https://github.com/nikolaydubina/jsonl-graph



## Web tools

* Kubernetes Instance Calculator
Tool to help you figure out what types of instances / instance groups you want to create based on your pod needs.
https://learnk8s.io/kubernetes-instance-calculator

# References

* Top Open Source Kubernetes Security Tools of 2021
Article from RedHat outlining several great security tools for your k8s cluster.
https://cloud.redhat.com/blog/top-open-source-kubernetes-security-tools-of-2021

* miniature-waffle
by 3sky. Repo has a good starting template for a terraform deploy of kuberentes. Referencing here because the base commands from creating the cluster, getting the correct kube-config, to pushing containers to your own ECR are spot on.
https://github.com/3sky/miniature-waffle

* Enabling graceful node shutdown on EKS in Kuberentes 1.21
Blog by Nik Skoufis on how to go into your nodes and modify kubelet to detect the node is about to be shutdown and enable "graceful" transfer of running pods.
https://blog.skouf.com/posts/enabling-graceful-node-shutdown-on-eks-in-kubernetes-1-21/

* Canary deployment with EKS
Repo from Jerome Decoster with an example on how to do canary deployments with EKS using scripts.
https://github.com/jeromedecoster/eks-canary

* Persistent Volumes Examples and Best Practices.
https://loft.sh/blog/kubernetes-persistent-volumes-examples-and-best-practices/

* Security Profiles Operator
Seccomp - security profiles for kubernetes resources. *Drastic over simplification
https://github.com/kubernetes-sigs/security-profiles-operator/blob/main/installation-usage.md

* Demystifying kube-proxy
In-depth but approachable blog on how pods get ip addresses and how iptables are manipulated.
https://mayankshah.dev/blog/demystifying-kube-proxy/
