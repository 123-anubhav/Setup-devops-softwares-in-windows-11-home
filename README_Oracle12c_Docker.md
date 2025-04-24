
# 🐳 Oracle 12c Setup Using Docker in Ubuntu VM (Recommended)

> ✅ Fully tested with `truevoly/oracle-12c` Docker image  
> ✅ Compatible with **Windows 11 Home** using **Ubuntu VM + Docker**

---

## 🚀 Steps to Setup Oracle 12c

### Step 1: Create Docker Volume

```bash
docker volume create oracle12c_data
```

### Step 2: Verify Volume Creation

```bash
docker volume ls
```

### Step 3: Pull the Oracle Docker Image

```bash
docker pull truevoly/oracle-12c
```

### Step 4: Run the Oracle Container

```bash
docker run -d \
  --name oracle12c \
  -p 1521:1521 \
  -p 8080:8080 \
  -e ORACLE_ALLOW_REMOTE=true \
  -e ORACLE_DISABLE_ASYNCH_IO=true \
  -v oracle12c_data:/u01/app/oracle \
  truevoly/oracle-12c
```

---

## 🔍 Explanation of Parameters

| Flag / Option                         | Description                                                                 |
|--------------------------------------|-----------------------------------------------------------------------------|
| `-d`                                 | Run container in detached mode                                             |
| `--name oracle12c`                   | Set the container name to `oracle12c`                                     |
| `-p 1521:1521`                       | Maps Oracle SQLNet port for SQL Developer                                 |
| `-p 8080:8080`                       | Maps web console port (Enterprise Manager, APEX)                          |
| `-e ORACLE_ALLOW_REMOTE=true`       | Allows remote DB connections from outside the container                   |
| `-e ORACLE_DISABLE_ASYNCH_IO=true`  | Avoids I/O errors on Windows/Mac                                          |
| `-v oracle12c_data:/u01/app/oracle` | Persists DB files, configs, and logs to local named Docker volume         |

---

## 🎯 After Running

- Oracle 12c starts automatically.
- Access **web console** (if configured): [http://localhost:8080/em](http://localhost:8080/em)
- Connect using SQL Developer:

  ```
  Host: localhost
  Port: 1521
  Service Name: xe
  Username: system
  Password: oracle
  ```

---

## 🛠️ Useful Docker Commands

```bash
# Stop the Oracle container
docker stop oracle12c

# Start the Oracle container again
docker start oracle12c

# Remove the Oracle container
docker rm -f oracle12c

# View logs
docker logs -f oracle12c
```

---
