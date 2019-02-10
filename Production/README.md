# Production
Production assets I should know!

## Table of Contents
1. [Kubernetes](#kubernetes)
## Kubernetes
### What is it? 
Kubernetes(K8S) is a platform for managing containers. 
It manages the deployment, scaling loading, monitering and logging of clusters.<br/>
Some terminology:
* Node - A node is a working machine(Virtual Machine or Physical Machine).
* Pod - The smallest peice of the K8s puzzle, pods run the application and the runtime env is commonly docker.
* Replication - Using multiple pods across multiple instances 1-1 (scaling horizontally).
### How?
Getting into the niddy griddy of how it works.<br/>
You have a master node that controls traffic flow to worker nodes routing traffic through K8s API.
