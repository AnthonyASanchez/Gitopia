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
### Kubernetes Deployment
In order to deploy an application you need to specify a 'Deployment Configuration'. Once this is defined the master 
controller will schedule the release to individual nodes in cluster. <br/>
Then a 'Kubernetes Deployment Controller' (KDC) will moniter the instances the application was deployed on. The KDC is 
then able to replace failing nodes with other working ones. Which is much better than DevOps having to manually deply another 
node.<br/>
How a deployed application looks.
![](https://github.com/AnthonyASanchez/Gitopia/blob/master/Production/imgs/kub_cluster.svg)
When runnning kubernetes on the cloud, you will commonly hear the os 'CoreOS', it is the leading container operating system that is designed to run at a massive scale.<br/>
