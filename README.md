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
  * Disable SELinux service
  * Disable Swapping on 
