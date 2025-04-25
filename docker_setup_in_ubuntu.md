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

And try with 
$ docker images
if you see after docker installation 
error:
docker images
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Head "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied

do it with sudo permission
$ sudo docker images

or

That error means your user doesn't have permission to access the Docker daemon. You have two options to fix it:

✅ Option 1: Run with sudo (Quick Fix)
Try this:

$ sudo docker images
But you'll need sudo every time unless you fix permissions.

✅ Option 2: Add Your User to the docker Group (Recommended)
This lets you run Docker commands without sudo.

Add your user to the Docker group:

$ sudo usermod -aG docker $USER
Apply the group change:

Either log out and log back in, or run:

$ newgrp docker
Test again:

$ docker images
You should no longer get the "permission denied" error.