# Docker Installation on Ubuntu 22.04.5 LTS

This guide provides step-by-step instructions to install Docker on Ubuntu 22.04.5 LTS.

---

## ✅ Step 1: Update Your System

```bash
sudo apt update
Why? Ensures your package list is up to date.

✅ Step 2: Install Required Packages
bash
Copy
Edit
sudo apt install apt-transport-https ca-certificates curl software-properties-common lsb-release gnupg -y
Why? Required to securely fetch Docker packages.

✅ Step 3: Add Docker’s Official GPG Key
bash
Copy
Edit
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
Why? Verifies package authenticity.

✅ Step 4: Add Docker Repository
bash
Copy
Edit
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
Why? Adds Docker packages to your system's sources.

✅ Step 5: Update Package Index Again
bash
Copy
Edit
sudo apt update
Why? To fetch packages from the Docker repo.

✅ Step 6: Install Docker Engine
bash
Copy
Edit
sudo apt install docker-ce docker-ce-cli containerd.io -y
Why? Installs Docker core components.

✅ Step 7: Start and Enable Docker
bash
Copy
Edit
sudo systemctl enable docker
sudo systemctl start docker
Why? Ensures Docker starts on system boot.

✅ Step 8: Check Docker Version and Status
bash
Copy
Edit
docker --version
sudo systemctl status docker
Why? Verifies installation and service status.

✅ Step 9: (Optional) Run Docker Without sudo
bash
Copy
Edit
sudo usermod -aG docker $USER
Then log out and log back in, or run:

bash
Copy
Edit
newgrp docker
Why? Allows running Docker commands without sudo.

✅ Step 10: Test Docker
bash
Copy
Edit
docker run hello-world
🛠️ Troubleshooting: Permission Denied Error
If you see the following error after Docker installation:

bash
Copy
Edit
docker images
You get:

perl
Copy
Edit
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: 
Head "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied
✅ Option 1: Run with sudo (Quick Fix)
bash
Copy
Edit
sudo docker images
You'll need to use sudo every time unless you fix permissions.

✅ Option 2: Add Your User to the docker Group (Recommended)
Add your user to the Docker group:

bash
Copy
Edit
sudo usermod -aG docker $USER
Apply the group change by logging out and back in, or run:

bash
Copy
Edit
newgrp docker
Try again:

bash
Copy
Edit
docker images
✅ You should no longer get the "permission denied" error.

🛠️ If You See “Permission Denied” Error
Try these:

Confirm your user is in the docker group:

bash
Copy
Edit
groups $USER
Should list docker in the output.

If it still fails, run:

bash
Copy
Edit
newgrp docker
or log out and log back in.
