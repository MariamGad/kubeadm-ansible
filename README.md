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
  * Add inventory file has all hosts
  ```
  [masters]
  master ansible_host=node_IP  ansible_user=root

  [workers]
  worker1 ansible_host=node_IP ansible_user=root
  ```
  
* ### Kubernetes master and worker nodes
  * in `/etc/hosts` add 
  ```
  master_IP   master    masternode_hostname
  worker_IP   worker    workernode_hostname
  ```
---

## Installation Steps
* ### Allow Firewall ports
  * ports needed to be opened on master node\
  ![image](https://user-images.githubusercontent.com/47721226/225149321-a780ba7e-4b79-4790-9938-b52b6e87289f.png)
  * ports needed to be opened on worker node\
  ![image](https://user-images.githubusercontent.com/47721226/225150309-f6c4f9d8-3df6-4a29-a33c-db7841e35e2a.png)\
note: you can also disable Firewall service instead 

* ### Configure Kubernetes dependencies 
  These configurations are done on both master and worker Kubernetes nodes
  * Disable `SELinux` service
  * Disable `Swapping on` 
  * Install `CRI-O` a Container runtime 
  * Install `Kubeadm` a CLI tool that will install and configure the various components of a cluster.
  * Install `kubelet` a system service that runs on all nodes and handles node-level operations.
  * Install `kubectl` a CLI tool used for issuing commands to the cluster through its API Server.
  
* ### Setting Up the Master Node
  * Initialize the cluster by running `kubeadm init`
  *  Create a `.kube` directory at `/home/cloud`. This directory will hold configuration information such as the admin key files, which are required to connect to the cluster, and the cluster’s API address.\
  **note: cloud is a non-root user should be added before**
  *  Copy the `/etc/kubernetes/admin.conf` file that was generated from `kubeadm init` to your non-root **cloud** user’s home directory.
  *  Run `kubectl apply` to install `Flannel`.
