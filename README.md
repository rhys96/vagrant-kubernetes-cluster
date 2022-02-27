# Kubernetes Cluster Using Ansible and Vagrant

__Note:__ This has only been tested on Ubuntu 20.04 LTS.

This project creates a local Kubernetes cluster for development purposes. This project is based on the blog post [Kubernetes Setup Using Ansible and Vagrant](https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/) by Kubernetes.

## Prerequisites
The following packages must be installed on your local machine:

|Name| Version|
|---|---|
| Virtual Box | 6.1.26 |
| Vagrant | 2.2.19 |
| Python | 3.8.10 |
| Ansible| 2.9.6 |

## Bringing Up The Cluster
To bring up the cluster, clone the following repository.
```
git clone https://github.com/rhys96/vagrant-kubernetes-cluster.git
```

Create and provision the virtual machines.
```
cd vagrant-kubernetes-cluster
vagrant up
```

Verify the cluster status.
```
vagrant ssh master

vagrant@master:~$ kubectl get nodes
NAME     STATUS   ROLES                AGE     VERSION
master   Ready    control-plane,master   14m     v1.23.4
node1    Ready    <none>                 8m59s   v1.23.4
node2    Ready    <none>                 3m57s   v1.23.4

```

## Navigating The Cluster
The cluster will bring up the following virtual machines:
|Hostname| IP Address| Role|
|---|---|---|
| master | 192.168.33.10 | Cluster Master |
| node`N` | 192.168.33.`{10+N}` | Cluster Node |

To SSH to the virtual machines, run the following command:
```
vagrant ssh <hostname>
```

To interact with the Kubernetes cluster, SSH to the master node.
```
vagrant ssh master

vagrant@master:~$ kubectl get nodes
NAME     STATUS   ROLES                AGE     VERSION
master   Ready    control-plane,master   14m     v1.23.4
node1    Ready    <none>                 8m59s   v1.23.4
node2    Ready    <none>                 3m57s   v1.23.4
```

In addition to `kubectl`, the master node includes `helm`. 

## Clean up
Destroy the cluster.
```
vagrant destroy
```

Remove the join-command file.
```
rm join-command
```
