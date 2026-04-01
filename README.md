# Assignment

In this assignment, we deployed a 3-node Kubernetes cluster using `kubeadm`. Due to limited resources and time constraints, no dedicated worker nodes were deployed.

## Comparison with Other Kubernetes Distributions

Compared to other Kubernetes distributions such as **kind** or **minikube**, `kubeadm` enables the deployment of a production-grade cluster when configured carefully.

With `kubeadm`, we can customize many parameters, including:

- **Networking CIDR** — allowing better integration with network devices  
- **etcd configuration** — enabling flexible cluster extension and migration  
- **Manual certificate approval** — improving cluster security  

## CNI Plugin Choice: Cilium

For the CNI plugin, we selected **Cilium**.

Cilium has gained popularity alongside the growth of Kubernetes-based data centers. By leveraging the **eBPF** feature of the Linux kernel, it provides faster and more flexible packet forwarding and filtering compared to traditional `iptables`-based CNI plugins.

Additional advantages of Cilium include:

- Enhanced **observability**
- Support for **egress control**
- Built-in **service mesh capabilities**
- Support for the **Gateway API**
- A dedicated **CLI tool**, which reduces learning and administrative overhead compared to other network plugins  

## Prerequisites

To successfully deploy the cluster using this repository, the following prerequisites must be met:

- 3 nodes running **Ubuntu Server**
- 1 bastion host running **Ansible**
- `kubeadm` installed on the bastion host
- `helm` installed on the bastion host  

## Preparation Steps

Before deploying the cluster, the following preparation steps are required:

1. Configure timezone and `ntp`
   ```bash
   ansible-playbook -i hosts --private-key ssh-key -K -b chrony.yaml -u k8s
   ```
2. Install necessary packages
   ```bash
   ansible-playbook -i hosts --private-key ssh-key -K -b k8s.yaml -u k8s
   ```

3. Add an Admin user and ssh harden  
   ```bash
   ansible-playbook -i hosts --private-key ssh-key -K -b adminuser.yaml -u k8s
   ```

## Cluster Initialization

To create the cluster:

1. Log in to one of the three nodes (the **bootstrap node**)  
2. Run the following command:

```bash
kubeadm init
