
# MySQL Installation and Configuration on WSL2 for Remote Access

## 1. Install MySQL on WSL2

Update package lists and install MySQL:

```bash
sudo apt update
sudo apt install mysql-server
```

## 2. Start MySQL and Enable It

Start the MySQL service and enable it to start on boot:

```bash
sudo service mysql start
sudo systemctl enable mysql
```

## 3. Secure MySQL Installation

Run the MySQL secure installation script to set a root password and secure your MySQL setup:

```bash
sudo mysql_secure_installation
```

During this process, you will:
- Choose 'Y' for VALIDATE PASSWORD plugin
- Choose a password strength level (1 is good for development)
- Set a strong root password
- Answer 'Y' to all other questions

## 4. Create MySQL User for Remote Access

Login to MySQL:

```sql
sudo mysql
```

Then run the following commands to create a new user and grant privileges:

```sql
CREATE USER 'aryan'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'aryan'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

# ✅Grant Global Privileges (One-Time Setup)

## 🔹 Full Access to All Databases
If you want `aryan` to automatically have **full access to all databases**, including future ones, run this command:

```sql
GRANT ALL PRIVILEGES ON *.* TO 'aryan'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
This gives `aryan` **full control over all current and future databases**.
---

## 🔹 Grant Only CREATE Privilege  
💡 If you only want `aryan` to **create new databases** but not have full access to all databases, grant just the `CREATE` privilege:

```sql
GRANT CREATE ON *.* TO 'aryan'@'%';
FLUSH PRIVILEGES;
```
---

## 🔹 Checking Current Privileges  
You can check what privileges `aryan` currently has by running:

```sql
SHOW GRANTS FOR 'aryan'@'%';
```

---

## 🔹 Additional Commands  
If you face permission issues, try:

- **Refreshing Privileges**  
  ```sql
  FLUSH PRIVILEGES;
  ```
  
- **Restarting MySQL Server**  
  ```bash
  sudo systemctl restart mysql
  ```

- **Checking User-Specific Privileges**  
  ```sql
  SELECT user, host FROM mysql.user WHERE user = 'aryan';
  ```
  If `aryan@localhost` has different permissions than `aryan@'%'`, grant privileges specifically for `localhost`:
  
  ```sql
  GRANT ALL PRIVILEGES ON *.* TO 'aryan'@'localhost' WITH GRANT OPTION;
  FLUSH PRIVILEGES;
  ```

---

🚀 **With these settings, `aryan` will have the required privileges for MySQL databases without needing manual grants every time!**


## 5. Configure MySQL for Remote Connections

Edit MySQL's configuration file to allow remote connections:

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Find and modify/add these lines:

```ini
bind-address = 0.0.0.0
mysqlx-bind-address = 0.0.0.0
port = 3306
socket = /var/run/mysqld/mysqld.sock
```

Save and close the file.

## 6. Restart MySQL

Restart the MySQL service to apply the changes:

```bash
sudo service mysql restart
```

## 7. Get WSL2 IP Address

To get your WSL2 IP address (for connecting remotely):

```bash
ip addr show eth0 | grep inet
```

## 8. Connect to MySQL Remotely

You can now connect to MySQL remotely using the username `aryan` and the password you set during user creation.

