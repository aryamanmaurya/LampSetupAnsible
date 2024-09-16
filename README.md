
# LAMP Stack with WordPress Setup Using Ansible

This project sets up a LAMP (Linux, Apache, MariaDB, PHP) stack along with WordPress on a CentOS/RHEL-based system using Ansible. The web server listens on port 4444, and the WordPress installation is served from /wordpress path.

## Requirements
- CentOS/RHEL-based system
- Ansible installed on the control node

## Features
- Apache and PHP installation
- MariaDB installation (manual database and user setup)
- Custom index.html page with a background and a heading
- PHP a.php file for displaying PHP information
- WordPress installation in /var/www/lamp-stack/wordpress
- Firewall configuration to open port 4444
- SELinux relabeling for HTTP access on port 4444

## Project Structure
- **Document Root**: /var/www/lamp-stack
- **Apache Configuration**: /etc/httpd/conf.d/lamp-stack.conf
- **PHP File**: /var/www/lamp-stack/a.php
- **WordPress Directory**: /var/www/lamp-stack/wordpress
- **Port**: 4444 (both firewall and SELinux policies are configured)

## Ansible Playbook

### Tasks Overview
**Install Apache, PHP, and MariaDB**:
- Installs required packages.

**Start Apache and MariaDB Services**:
- Ensures both services are running and enabled.

**Set up Document Root**:
- Creates the /var/www/lamp-stack directory.

**Create index.html File**:
- Adds an HTML file with a background and heading to the document root.

**Create a.php File**:
- Adds a PHP info file (a.php) for testing PHP installation.

**Download and Extract WordPress**:
- Downloads and extracts WordPress in /var/www/lamp-stack/wordpress.

**Apache Configuration**:
- Configures Apache to serve the LAMP stack and WordPress on port 4444.

**Set Ownership**:
- Ensures Apache owns the document root.

**Open Firewall Port**:
- Opens port 4444 in the system firewall.

**Relabel SELinux Port**:
- Relabels port 4444 for HTTP access in SELinux.

**Restart Apache**:
- Restarts the Apache service to apply the changes.

## Manual Steps

### MariaDB Setup:
You need to manually create the database and user for WordPress using the following commands:

```bash
# Start MariaDB shell
sudo mysql -u root

# Create database and user
CREATE DATABASE wordpress_db;
CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## Access
- **LAMP Stack Home**: http://localhost:4444
- **WordPress Setup**: http://localhost:4444/wordpress
- **PHP Info**: http://localhost:4444/a.php

## Usage

Clone the repository:

```bash
git clone git@github.com:aryamanmaurya/LampSetupAnsible.git
cd LampSetupAnsible
```

Run the playbook:

```bash
ansible-playbook main.yaml -i <inventory-file>   # You will need to setup your own inventory-file.
```

Access the LAMP stack, WordPress, or PHP info from the browser.

## License
This project is licensed under the MIT License.
