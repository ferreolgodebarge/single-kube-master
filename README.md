# Deploy a single master Kubernetes Cluster with Ansible

## Objective

The goal is to deploy a 3 nodes Kubernetes cluster.
The cluster will contain a master node, a worker node, and a proxy node.

Nodes :

- Master node: contains all master node components (api-server, api-controller...)
- Worker node: contains all woker node components (kubelet) and hosts services
- Proxy node: is a specific worker node dedicated to ingress controller (Reverse proxy)

## Requirements

### Infrastructure

Minimal infrastructure requirements:

- one master node (Ubuntu 18.04, 2vCPU / 2GB RAM)
- at least one proxy node (Ubuntu 18.04, 1vCPU / 1GB RAM)
- at least one worker node (Ubuntu 18.04, 1vCPU / 1GB RAM)
- one local Linux environment to execute ansible playbooks

### Local environment

You will need python3, pip3 and ansible.

## Getting started

1. Clone this repository

```
$ git clone https://github.com/ferreolgodebarge/single-kube-master.git
$ cd single-kube-master
```

2. Create a virtualenv

```
$ virtualenv venv
```

3. Activate it

```
$ . venv/bin/activate
```

4. Install ansible

```
$ pip install ansible
```

5. Create a file env.sh containing your hosts IPs and ssh private key file

```bash
export KUBE_SSH_KEY="/path/to/private/key" 
export KUBE_MASTER_HOST1="master_hostname_or_ip"
export KUBE_PROXY_HOST1="proxy_hostname_or_ip"
export KUBE_WORKER_HOST1="worker_hostname_or_ip"
```

6. Source it

```
$ . env.sh
```

7. Run ansible playbook

```
$ ansible-playbook -i kubernetes/inventory/hosts kubernetes/single-master.yml
$ ansible-playbook -i kubernetes/inventory/hosts kubernetes/proxy.yml
$ ansible-playbook -i kubernetes/inventory/hosts kubernetes/workers.yml
```


