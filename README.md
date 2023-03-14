# kubeadm-ansible
## Overview
Create Kubernetes Cluster with Kubeadm using ansible on CentOS 8\
[Kubernetes](https://kubernetes.io/) is a container orchestration system that manages containers at scale.\
[Kubeadm](https://kubernetes.io/docs/reference/setup-tools/kubeadm/) automates the installation and configuration of Kubernetes components such as the API server, Controller Manager, and Kube DNS. 

---

## Prerequisite
* ### Ansible master node 
  * Install python3 `sudo yum install python3`
  * Install git `sudo yum install git`
  * Install ansible `sudo yum install epel-release` , `sudo yum install ansible`
  * Set Passwordless authentication between master and hosts (kuberenetes nodes) `ssh-keygen` , `ssh-copy-id root@IP_address`
  
* ### Kubernetes master and worker nodes
  * in `/etc/hosts` add 
  ```
  master_IP   master    masternode_hostname
  worker_IP   worker    workernode_hostname
  ```
---

## Installation Steps
