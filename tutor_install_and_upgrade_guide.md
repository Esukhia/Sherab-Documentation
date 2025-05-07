
# Tutor Installation and Database Restoration Guide

This document provides step-by-step instructions for installing Tutor, restoring your MySQL and MongoDB databases, and upgrading Tutor to the latest version.

---

## 1. Install Tutor

```bash
pip install "tutor[full]==16.1.8"
```

---

## 2. Launch Tutor in Development Mode

```bash
tutor dev launch
```

---

## 3. Restore the MySQL and MongoDB Databases

### MySQL

You will need the **SQL database dump** file and the **MySQL root password**.

```bash
cat path/to/sql/dump | docker exec -i <sql_container_id> /usr/bin/mysql -u root --password='your_sql_root_password' mysql
```

> Replace `<sql_container_id>` and `'your_sql_root_password'` with your actual values.

### MongoDB

1. Copy your MongoDB backup to:
   ```bash
   $TUTOR_ROOT/data/mongodb
   ```
2. Run:
   ```bash
   tutor dev exec mongodb bash
   ```
3. Then inside the container:
   ```bash
   mongorestore /data/db/db_name.mongodb/
   ```

---

## 4. Update MySQL Root Password in Configuration

Edit the file `$TUTOR_ROOT/config.yml` and set:

```yaml
MYSQL_ROOT_PASSWORD: your_sql_root_password
```

---

## 5. Rebuild the Open edX Image

```bash
tutor images build openedx --no-cache
```

---

## 6. Restart and Verify

```bash
tutor dev restart
# Verify the system is working correctly
tutor dev stop
```

---

## 7. Gradually Upgrade Tutor Version-by-Version

### Upgrade to Tutor 17

```bash
pip install --upgrade "tutor[full]>=17.0.0,<18.0.0"
tutor config save
tutor dev upgrade --from=palm
```

### Upgrade to Tutor 18

```bash
pip install --upgrade "tutor[full]>=18.0.0,<19.0.0"
tutor config save
tutor dev upgrade --from=quince
```

### Upgrade to Tutor 19

```bash
pip install --upgrade "tutor[full]>=19.0.0,<20.0.0"
tutor config save
tutor dev upgrade --from=redwood
```

---

## 8. Final Launch

```bash
tutor dev launch
```

> Ignore the following warning:
> 
> _It is recommended to upgrade your character set and collation of the MySQL database after upgrading to Sumac._  
> You can use the `convert-mysql-utf8mb4-charset` job to upgrade the collation and character set.  
> More details: [Tutor Docs - Changing the MySQL Charset and Collation](https://docs.tutor.edly.io/local.html#changing-the-mysql-charset-and-collation)
