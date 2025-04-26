
# Docker Installation on Ubuntu 22.04.5 LTS

This guide provides step-by-step instructions to install Docker on Ubuntu 22.04.5 LTS.

---

## ✅ Step 1: Update Your Packages
```bash
sudo apt update
sudo apt upgrade -y
```

---

## ✅ Step 2: Install Required Dependencies
```bash
sudo apt install ca-certificates curl gnupg lsb-release -y
```

---

## ✅ Step 3: Add Docker’s Official GPG Key
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

---

## ✅ Step 4: Set Up the Docker Repository
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

## ✅ Step 5: Update Package Index Again
```bash
sudo apt update
```

---

## ✅ Step 6: Install Docker Engine
```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

---

## ✅ Step 7: Verify Docker Installation
```bash
sudo docker --version
sudo docker run hello-world
```

---

## ✅ Step 8 (Optional): Run Docker Without `sudo`
```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

> ✅ **Note**: This will not harm your hardware. Docker is a containerization tool and works at the software level.
