# assignment
In this assignment, we deployed a 3 nodes kubernetes cluster with kubeadm. Due to the lack of resources and time limit, no dedicated worker nodes are deployed.

Comparing to other k8s distributions, such as kind or minikube, it is possible to deploy a production grade cluster with kubeadm when given careful consideration. With kubeadm, we are able to configure many parameters, such as networking CIDR, providing better integration with network devices, etcd connection, providing flexible extension and migration of the cluster, and munual certificate approval, making the cluster more secure. 
For cni plugin, we have chosen cilium. Cilium has gained popularity with the expansion of kubernetes based data center in recent years. Leveraging ebpf feature from Linux Kernel, it provides faster and flexible package forwarding and filtering comparing to iptable based cni plugins. Besides, it provides more feature than some other cni plugins such as observability, egress, service mesh and even Gateway API. Last but not least, it comes with a CLI tool, which greatly reduce the learning and administration overhead comparing to other network plugins.

For successful deployment for the cluster with this repository, following prerequisite should be satisfied:
3 Nodes running ubuntu server;
1 Bastion host running ansible;
kubeadm should be installed on Bastion host;
helm chart should be installed on Bastion host;

Before deploying the cluster, there are several steps for preparation:
chrony setting
ansible-playbook
kubernetes preparation
ansible-playbook

to create the cluster, we will need to login to one of the 3 nodes (bootstrapper) and run kubeadm init command