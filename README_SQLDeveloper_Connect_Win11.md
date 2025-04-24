
# How to Connect Using SQL Developer from Windows 11 Home

📅 **23 April 2025**  
🕒 **15:25**

## 📘 Overview
This guide walks you through how to connect to Oracle 12c using SQL Developer on a Windows 11 Home system.

---

## 🔸 Step 1: Open SQL Developer
Make sure you have installed the **Windows 64-bit with JDK 17 included** version of SQL Developer.

---

## 🔸 Step 2: Create a New Connection

1. Open SQL Developer.
2. Click on **New Connection** (top left corner or go to `File → New → Database Connection`).
3. Fill in the connection details as follows:

| Field             | Value                  |
|------------------|------------------------|
| Connection Name   | Oracle12cLocal (or any name you prefer) |
| Username          | system                 |
| Password          | oracle                 |
| Hostname          | localhost              |
| Port              | 1521                   |
| SID or Service    | Choose **Service Name** and type `xe` |

✅ Optionally check **Save Password** if you want to store the credentials.

---

## 🔸 Step 3: Test & Connect

- Click on the **Test** button.
  - If everything is correct, it will show: **Status: Success 💚**
- Click **Connect** to proceed.

---

## 🔸 Bonus: Access GUI Consoles (Optional)

Open the following URLs in your browser:

- **APEX**: [http://localhost:8080/apex](http://localhost:8080/apex)
- **Enterprise Manager**: [http://localhost:8080/em](http://localhost:8080/em)

If login is requested, use:

- **Username**: `system`  
- **Password**: `oracle`  
- **Service Name**: `xe`

---

✅ You're all set to use Oracle 12c via SQL Developer on your Windows 11 Home system!
