
# Kubernetes Installation Guide on Ubuntu

## Prerequisites

- **Ubuntu 22.04.5 LTS** installed on the VM.
- **Docker** installed and running.
- Sufficient permissions (root or sudo) to install software.
- Basic knowledge of Linux terminal commands.

## 1. Update the System

First, ensure that your system is up-to-date:

```bash
sudo apt-get update && sudo apt-get upgrade -y
```

## 2. Install Prerequisites

Install required dependencies:

```bash
sudo apt-get install -y apt-transport-https ca-certificates curl
```

## 3. Add Kubernetes Package Repository

Download and add Kubernetes GPG key:

```bash
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
```

Add Kubernetes repository:

```bash
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

## 4. Install Kubernetes Components

Install Kubernetes tools:

```bash
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
```

Mark the Kubernetes components to prevent upgrades:

```bash
sudo apt-mark hold kubelet kubeadm kubectl
```

## 5. Disable Swap

Kubernetes does not support swap memory. Disable it using:

```bash
sudo swapoff -a
```

Make the change permanent:

```bash
sudo sed -i '/ swap / s/^\(.*\)$/#/g' /etc/fstab
```

## 6. Initialize Kubernetes Master Node

Run the following command to initialize the Kubernetes master node:

```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```

If successful, you'll see a message with instructions to set up `kubectl` access for your user. Follow these commands:

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Alternatively, if you are the root user, you can run:

```bash
export KUBECONFIG=/etc/kubernetes/admin.conf
```

## 7. Install Pod Network Add-on

To deploy the pod network, apply the following YAML manifest:

```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

## 8. Verify Kubernetes Cluster

Check the status of your cluster:

```bash
kubectl get nodes
kubectl get pods --all-namespaces
```

The nodes should show up as `Ready`, and pods should be in `Running` state.

## 9. Join Worker Nodes (Optional)

If you have worker nodes, join them to the cluster using the command shown in the `kubeadm init` output. It should look something like this:

```bash
kubeadm join <Master-IP>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

---

## Docker Setup

### 1. Install Docker

If Docker is not installed, run the following command:

```bash
sudo apt-get install -y docker.io
```

### 2. Verify Docker Installation

Check Docker status:

```bash
sudo systemctl start docker
sudo systemctl enable docker
docker --version
docker ps
```

---

## Notes

- Kubernetes no longer uses Docker as the container runtime by default. It uses **containerd**.
- Reinstalling Docker on your system should not affect the running Kubernetes cluster, as Kubernetes uses containerd internally.
- Make sure Docker is running properly for other tasks, but Kubernetes will continue working with containerd.

---

Happy Kubernetes Setup! 🎉
