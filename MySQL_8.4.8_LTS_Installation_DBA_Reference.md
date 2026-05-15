# MySQL 8.4 LTS — Senior DBA Quick Reference

> **Version:** MySQL 8.4.x LTS | **Platform:** Ubuntu 22.04 | **Last Updated:** 2026-05

---

## 1. Installation

> **⚠️ Method Note:** The manual tarball/`dpkg -i *.deb` method works but is **not recommended for production**.
> It gives you no upgrade path — security patches require a full manual re-download each time.
> The correct method for any real server is Oracle's **MySQL APT Repository**, documented below.

### 1.1 Add the Oracle MySQL APT Repository

```bash
# 1. Update the system first
sudo apt update && sudo apt upgrade -y

# 2. Download the MySQL APT config package from Oracle
#    Always check https://dev.mysql.com/downloads/repo/apt/ for the latest config .deb
wget https://dev.mysql.com/get/mysql-apt-config_0.8.28-1_all.deb

# 3. Install the config package — an interactive dialog will appear
sudo dpkg -i mysql-apt-config_0.8.28-1_all.deb
```

When the interactive dialog appears:
- Select **"MySQL Server & Cluster"**
- Choose **`mysql-8.4-lts`** as the version
- Navigate to **OK** and press Enter

```bash
# 4. Refresh APT to include the new Oracle repository
sudo apt update

# 5. Install MySQL Community Server
sudo apt install mysql-community-server
# You will be prompted to set the root password and choose an auth plugin.
# Choose: "Use Strong Password Encryption" (caching_sha2_password) — RECOMMENDED
```

### 1.2 Pin the Version (Critical for Production)

Prevent `apt upgrade` from accidentally jumping to MySQL 9.x:

```bash
sudo tee /etc/apt/preferences.d/mysql <<'EOF'
Package: mysql-server mysql-community-server
Pin: version 8.4.*
Pin-Priority: 1001
EOF
```

> **DBA Note:** This is non-negotiable in production. Without pinning, a routine `apt upgrade`
> could trigger a major-version upgrade mid-deployment. Always pin and upgrade MySQL deliberately
> during a planned maintenance window.

### 1.3 Applying Future Security Patches

With the APT repo in place, all future 8.4.x patch releases are trivial:

```bash
sudo apt update && sudo apt upgrade
```

> **DBA Note:** Oracle's LTS policy provides **5 years of Premier Support** and **3 years of
> Extended Support** for MySQL 8.4. Security patches will be regular — with the APT repo,
> they apply in seconds rather than manual re-installs.

---

## 2. Post-Installation Verification

```bash
# Verify the service is running
sudo systemctl status mysql

# Confirm the installed version
mysqld --version

# Confirm APT knows about the Oracle repo (should show repo.mysql.com as source)
apt-cache policy mysql-community-server

# Enable auto-start on boot (if not already enabled)
sudo systemctl enable mysql
```

---

## 3. Secure the Installation

Run the security hardening script immediately after install:

```bash
sudo mysql_secure_installation
```

### Interactive Prompts

| Prompt | Recommended Input | Notes |
|--------|------------------|-------|
| Validate Password Component | `Y` | Enforces password policy |
| Password Strength Level | `2` (High) | `0`=Low, `1`=Medium, `2`=High |
| Remove anonymous users | `Y` | Eliminates unauthenticated access |
| Disallow root remote login | `Y` | Root should never log in remotely |
| Remove test database | `Y` | Test DB is a security liability |
| Reload privilege tables | `Y` | Applies changes immediately |

> **DBA Note:** In production, always use level `2` (High) password strength. Store the root
> password in your organisation's secrets manager (e.g., HashiCorp Vault, AWS Secrets Manager)
> — never in plaintext.

---

## 4. Connecting to the MySQL Server

```bash
# Connect as root
mysql -u root -p
# Enter password when prompted
```

```sql
-- Verify running version
SELECT VERSION();

-- List all databases
SHOW DATABASES;
```

---

## 5. User Management

### 5.1 Log In as Root

```bash
sudo mysql -u root -p
```

### 5.2 Create a User

```sql
-- Localhost only (preferred for app users)
CREATE USER 'username'@'localhost' IDENTIFIED BY 'StrongPassword!';

-- Allow from any host (use sparingly — only for replication/remote access)
CREATE USER 'username'@'%' IDENTIFIED BY 'StrongPassword!';
```

> **DBA Note:** Prefer `'username'@'localhost'` or `'username'@'<specific_ip>'` over `'%'`.
> Wildcard hosts dramatically increase the attack surface.

### 5.3 Grant Privileges

```sql
-- Full access to a specific database (dev/staging environments)
GRANT ALL PRIVILEGES ON dbname.* TO 'username'@'localhost';

-- Least-privilege access (recommended for production app users)
GRANT SELECT, INSERT, UPDATE ON dbname.* TO 'username'@'localhost';
```

> **DBA Note:** Follow the **principle of least privilege**. Application users rarely need
> `DELETE`, `DROP`, or `ALTER`. Grant only what the app explicitly requires.

### 5.4 Apply Permission Changes

```sql
-- Reload the grant tables to apply changes immediately
FLUSH PRIVILEGES;
```

### 5.5 Verify & Audit User Grants

```sql
-- View all users in the system
SELECT user, host FROM mysql.user;

-- Inspect grants for a specific user
SHOW GRANTS FOR 'username'@'localhost';
```

### 5.6 Revoke or Drop a User (Housekeeping)

```sql
-- Revoke specific privileges
REVOKE INSERT, UPDATE ON dbname.* FROM 'username'@'localhost';

-- Remove a user entirely
DROP USER 'username'@'localhost';
```

---

## 6. Logging In as a Non-Root User

```bash
# Shell
mysql -u <username> -p
# Enter password
```

```sql
-- Switch to target database
USE dbname;

-- List tables
SHOW TABLES;
```

---

## 7. DBA Quick-Reference Cheatsheet

```sql
-- Show all running processes
SHOW PROCESSLIST;

-- Check global variables (e.g., max connections)
SHOW GLOBAL VARIABLES LIKE 'max_connections';

-- Check current connection count
SHOW STATUS LIKE 'Threads_connected';

-- Show InnoDB engine status (for lock/deadlock analysis)
SHOW ENGINE INNODB STATUS\G

-- List all databases with sizes
SELECT table_schema AS 'Database',
       ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) AS 'Size (MB)'
FROM information_schema.tables
GROUP BY table_schema;
```

---

## 8. Key Config File Locations

| File/Directory | Purpose |
|----------------|---------|
| `/etc/mysql/mysql.conf.d/mysqld.cnf` | Primary server configuration |
| `/etc/apt/preferences.d/mysql` | APT version pin file |
| `/var/log/mysql/error.log` | Error log |
| `/var/lib/mysql/` | Data directory |
| `/var/run/mysqld/mysqld.sock` | Unix socket |

---

## 9. Installation Method Comparison

| | Manual Tarball (Old Method) | APT Repository (Correct Method) |
|---|---|---|
| **Source** | Manual download from mysql.com | Oracle's official APT repo |
| **Security patches** | Manual re-download every time | `apt update && apt upgrade` |
| **Version pinning** | No control | `/etc/apt/preferences.d/` |
| **Upgrade path** | Manual, error-prone | Fully managed by apt |
| **Boot auto-start** | Must configure manually | Handled by package install |
| **Production safe?** | Dev/test only | Yes |
| **Recommended by Oracle?** | No | Yes |

---

*Generated for personal DBA reference. Always test commands in a non-production environment first.*
