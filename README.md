# AKS-test-lab---cheap-
The aim of this project is to create and run an AKS cluster (S) as cheaply as possibly for testing workloads and configurations. This is based on the following article: 
https://techcommunity.microsoft.com/t5/azure-developer-community-blog/tip-running-a-cheap-aks-lab/ba-p/1407997

Benefits of such a setup

Cost-friendly, providing you do not let ACIs hanging around
Allows for resource-greedy scenarios 
 

Limitations of such a setup

 

Although interesting from a financial perspective, it comes with a few limitations:


Suitable for lab-only activities
Suitable for short-running containers (again, perfect in a demo scenario, etc.). When used like this, you might end up with only a few euros/dollars to pay at the end of the month instead of much more for a full blown worker node.
Container startup is a little delayed because of the ACI provisioning.
By default, only 100 concurrent ACIs are allowed per subscription, meaning that you can't have more than 100 concurrent pods. This can be changed by reaching out to support.
Make sure to clean your stuff after use, else the ACIs will keep running forever which then will become very costly. The easiest way is to run a kubectl delete namespace .... but the bare minimum is to run a kubectl scale deploy --all --replicas=0 so as to let AKS destroy the corresponding ACIs. 
To wrap it up, to get a cheap AKS lab, just proceed the following steps:

Create the cluster & enable Virtual Nodes
Choose the smallest possible VM as your main worker node
