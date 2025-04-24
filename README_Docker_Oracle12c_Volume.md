
# Use Same Data File Using Docker Volume

**24 April 2025**  
**16:46**  

---

## ✅ Scenario:
You stop and delete the container:

```bash
docker stop oracle12c
docker rm oracle12c
```

Then recreate it with the same volume name:

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

### ✅ Result:
Oracle will boot up and use the same database files inside `oracle12c_data`, and your data will be preserved.

---

## ⚠️ Your Data Will NOT Persist If:
- You use a different volume name.  
- You run without `-v oracle12c_data:/u01/app/oracle`.  
- You explicitly delete the volume:

```bash
docker volume rm oracle12c_data
```
