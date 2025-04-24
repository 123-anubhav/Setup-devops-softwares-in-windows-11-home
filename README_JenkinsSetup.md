
# Jenkins Setup in Ubuntu Docker Environment

This guide provides step-by-step instructions to set up Jenkins in a Docker container on an Ubuntu machine.

---

## 🚀 Steps to Setup Jenkins

### 1. Pull the Jenkins Docker Image

```bash
docker pull jenkins/jenkins:lts
```

This pulls the Long-Term Support (LTS) version of Jenkins.

---

### 2. Run Jenkins in a Docker Container

```bash
docker run -d --name jenkins -p 8080:8080 jenkins/jenkins:lts
```

- `-d`: Run the container in detached mode.
- `--name jenkins`: Names the container "jenkins".
- `-p 8080:8080`: Maps host port 8080 to container port 8080.

---

### 3. Access Jenkins UI

Open your browser and go to:

```
http://localhost:8080/
```

You will be prompted to enter an **Administrator password**.

---

### 4. Retrieve the Initial Admin Password

To get the password, run:

```bash
docker logs jenkins
```

Look for a line in the output similar to this:

```plaintext
*************************************************************
Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

1234567890abcdef1234567890abcdef
*************************************************************
```

Copy the password and paste it into the Jenkins UI to complete the setup.

---

## 🎉 That's It!

You've successfully set up Jenkins in Docker on Ubuntu! Enjoy building, testing, and deploying with Jenkins.

---
