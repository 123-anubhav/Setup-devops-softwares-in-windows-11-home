# Docker Installation on Ubuntu 22.04.5 LTS

This guide provides step-by-step instructions to install Docker on Ubuntu 22.04.5 LTS.

---

## 🚀 **Step 1: Update Your System**

To ensure your package list is up to date:

```bash
sudo apt update
📦 Step 2: Install Required Packages
Install the necessary packages to securely fetch Docker packages:

bash
Copy
Edit
sudo apt install apt-transport-https ca-certificates curl software-properties-common lsb-release gnupg -y
🔑 Step 3: Add Docker’s Official GPG Key
This command will add Docker's official GPG key to verify package authenticity:

bash
Copy
Edit
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
🏁 Step 4: Add Docker Repository
Add the Docker repository to your system's sources list:

bash
Copy
Edit
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
🔄 Step 5: Update Package Index Again
Update your package list to fetch packages from the Docker repository:

bash
Copy
Edit
sudo apt update
🛠 Step 6: Install Docker Engine
Now, install the core Docker components:

bash
Copy
Edit
sudo apt install docker-ce docker-ce-cli containerd.io -y
🚀 Step 7: Start and Enable Docker
Enable Docker to start automatically at boot, and then start the Docker service:

bash
Copy
Edit
sudo systemctl enable docker
sudo systemctl start docker
✔️ Step 8: Check Docker Version and Status
Verify Docker installation and check its service status:

bash
Copy
Edit
docker --version
sudo systemctl status docker
⚙️ Step 9: Run Docker Without sudo (Optional)
To avoid using sudo for every Docker command, add your user to the docker group:

bash
Copy
Edit
sudo usermod -aG docker $USER
Then log out and log back in, or run:

bash
Copy
Edit
newgrp docker
🏁 Step 10: Test Docker
Finally, test the installation by running a simple Docker container:

bash
Copy
Edit
docker run hello-world
🚧 Troubleshooting: Permission Denied Error
If you encounter a "permission denied" error when running Docker commands, it may look like this:

bash
Copy
Edit
docker images
perl
Copy
Edit
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: 
Head "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied
🛠 Option 1: Run with sudo (Quick Fix)
You can always run Docker with sudo as a quick workaround:

bash
Copy
Edit
sudo docker images
Note: You will need to use sudo every time unless you resolve the permission issue.

🛠 Option 2: Add Your User to the docker Group (Recommended)
To resolve the issue more permanently, add your user to the Docker group:

Add your user to the Docker group:

bash
Copy
Edit
sudo usermod -aG docker $USER
Apply the group change by logging out and logging back in, or run:

bash
Copy
Edit
newgrp docker
After this, try running Docker again:

bash
Copy
Edit
docker images
✅ You should no longer encounter the "permission denied" error.

🛠️ If You See “Permission Denied” Error Even After Adding to Docker Group
Try the following steps:

Confirm your user is in the docker group by running:

bash
Copy
Edit
groups $USER
This should list docker in the output.

If it still doesn’t work, apply the group change using:

bash
Copy
Edit
newgrp docker
Alternatively, log out and log back in to apply the changes.

