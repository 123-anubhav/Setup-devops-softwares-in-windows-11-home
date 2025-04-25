# Docker Installation on Ubuntu 22.04.5 LTS

This guide provides step-by-step instructions to install Docker on Ubuntu 22.04.5 LTS.

---

## ✅ Step 1: Update Your System

```bash
sudo apt update
```

**Why?** Ensures your package list is up to date.

---

## ✅ Step 2: Install Required Packages

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common lsb-release gnupg -y
```

**Why?** Required to securely fetch Docker packages.

---

## ✅ Step 3: Add Docker’s Official GPG Key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

**Why?** Verifies package authenticity.

---

## ✅ Step 4: Add Docker Repository

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

**Why?** Adds Docker packages to your system's sources.

---

## ✅ Step 5: Update Package Index Again

```bash
sudo apt update
```

**Why?** To fetch packages from the Docker repo.

---

## ✅ Step 6: Install Docker Engine

```bash
sudo apt install docker-ce docker-ce-cli containerd.io -y
```

**Why?** Installs Docker core components.

---

## ✅ Step 7: Start and Enable Docker

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

**Why?** Ensures Docker starts on system boot.

---

## ✅ Step 8: Check Docker Version and Status

```bash
docker --version
sudo systemctl status docker
```

**Why?** Verifies installation and service status.

---

## ✅ Step 9: (Optional) Run Docker Without `sudo`

```bash
sudo usermod -aG docker $USER
```

Then log out and log back in, or run:

```bash
newgrp docker
```

**Why?** Allows running Docker commands without `sudo`.

---

## ✅ Step 10: Test Docker

```bash
docker run hello-world
```
