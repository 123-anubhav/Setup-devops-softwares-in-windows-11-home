
# Install Kubernetes on Master Node

## 🔒 Create Security Group
✅ Create a security group with the following inbound rules:

- **Rule 1:**  
  - Type: SSH (22)  
  - Source: Anywhere

- **Rule 2:**  
  - Type: ALL TCP  
  - Source: Anywhere

## 🖥️ Create Virtual Machines
✅ Launch 3 Virtual Machines using Ubuntu 20.04 AMI:  
(You can use Ubuntu 24 also — it works. Avoid Ubuntu 22, it causes connection refused issues.)

- 1 Master Node: `t2.medium`
- 2 Worker Nodes: `t2.micro`

## 🛠️ Common Setup on Master & Worker Nodes

### Update and Prepare the System
```bash
sudo apt-get update
```

### Configure Containerd
```bash
cat <<EOF | sudo tee /etc/modules-load.d/containerd.conf
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter
```

### System Config for Kubernetes Networking
```bash
cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF

sudo sysctl --system
```

### Install Containerd
```bash
sudo apt-get update
sudo apt-get install -y containerd

sudo mkdir -p /etc/containerd
sudo containerd config default | sudo tee /etc/containerd/config.toml
sudo systemctl restart containerd
sudo systemctl status containerd
```

### Disable Swap
```bash
sudo swapoff -a
sudo sed -i '/ swap / s/^\(.*\)$/#/g' /etc/fstab
```

### Install Dependencies
```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https curl
```

## 📦 Add Kubernetes Repository

Add Kubernetes APT Repository:
```bash
sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
```

## 📥 Install Kubernetes Packages
```bash
sudo apt-get install -y kubelet kubeadm kubectl kubernetes-cni nfs-common
sudo apt-mark hold kubelet kubeadm kubectl kubernetes-cni nfs-common
```

## 🧠 Master Node Setup

### Initialize Kubernetes Cluster
```bash
sudo kubeadm init
```

⚠️ **Important:** If you get `[ERROR NumCPU]: the number of available CPUs 1 is less than the required 2`, use:

```bash
sudo kubeadm init --ignore-preflight-errors=NumCPU
```

### Configure Kubectl Access
```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Check node status:
```bash
kubectl get nodes
```

### Install Calico Network Add-On
```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
kubectl get nodes
```

## 🔗 Join Worker Nodes to Cluster

### On Master Node, generate the join command:
```bash
kubeadm token create --print-join-command
```

### On Worker Nodes, run the join command:
```bash
sudo kubeadm join <master-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

### On Master Node, verify cluster status:
```bash
kubectl get nodes
```
