🚀 Docker Installation on Ubuntu 22.04.5 LTS
This guide provides step-by-step instructions to install Docker on Ubuntu 22.04.5 LTS and configure it to run without sudo.

✅ Step 1: Update Your System
bash
Copy
Edit
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
✅ Step 9: Run Docker Without sudo
bash
Copy
Edit
sudo usermod -aG docker $USER
Then apply group changes without logout:

bash
Copy
Edit
newgrp docker
Why? This lets you run Docker without always needing sudo.

✅ Step 10: Test It Out
bash
Copy
Edit
docker run hello-world
docker images
✅ You should not need sudo anymore.

🛠️ If You See “Permission Denied” Error
Try these:

Confirm your user is in the docker group:

bash
Copy
Edit
groups $USER
Should list docker.

If it still fails:

bash
Copy
Edit
newgrp docker
or log out and log back in.
