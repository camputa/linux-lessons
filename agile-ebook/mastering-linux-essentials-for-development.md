# Onboarding Guide: Mastering Linux Essentials for Development

Welcome to our team! I'm excited to guide you through our essential Linux skills on Ubuntu. This guide is designed to empower you with practical knowledge for navigating the Linux terminal, managing files and directories efficiently, and performing system administration tasks. On completing this guide, you'll be equipped to navigate our Linux development environment confidently and contribute effectively to our projects.

## Introduction

Our objective is to equip you with the foundational skills required to thrive in our dynamic technology environment. This guide covers essential Linux commands, file management, user administration, and web server configuration, ensuring you have the tools and knowledge to contribute effectively to our projects. By the end of this training, you will be adept at navigating and managing a Linux-based development environment, enhancing both your personal growth and our team’s success.

---

## Basic Navigation

Navigating the Linux file system efficiently is fundamental for any developer or system administrator. The `ls` and `cd` commands are among the most frequently used commands in the terminal. Here, we’ll explore these commands with their common options and practical usage examples.

---

### [ls] Command: Listing Directory Contents

The `ls` command is used to list the contents of a directory. It provides various options to customize the output based on your needs.

- **Basic Usage**:

  ```bash
  ls
  ```

  Lists files and directories in the current working directory.

- **Common Options**:

  - `-l`: Long listing format. Displays detailed information including permissions, owner, group, size, and modification date.

    ```bash
    ls -l
    ```

  - `-a`: Displays all files, including hidden files (those starting with `.`).

    ```bash
    ls -a
    ```

  - `-h`: Human-readable format. Converts file sizes into a more readable format (e.g., KB, MB, GB).

    ```bash
    ls -lh
    ```

  - **Example Output**:

    ```
    -rw-r--r-- 1 user user  512 Jul 14 10:05 file.txt
    drwxr-xr-x 2 user user 4.0K Jul 14 10:00 Documents
    ```

---

### [cd] Command: Changing Directories

The `cd` command allows you to change your current working directory within the file system.

- **Basic Usage**:

  ```bash
  cd directory_name
  ```

  Changes the current directory to `directory_name`.

- **Special Directories**:

  - `~`: Home directory of the current user.

    ```bash
    cd ~
    ```

  - `..`: Moves up one directory level (parent directory).

    ```bash
    cd ..
    ```

  - `.`: Represents the current directory.

    ```bash
    cd .
    ```

- **Navigating to a Specific Path**:

  ```bash
  cd /path/to/directory
  ```

  Changes the current directory to the specified path.

- **Examples**:

  - Navigate to the home directory:

    ```bash
    cd ~
    ```

  - Move up one level from the current directory:

    ```bash
    cd ..
    ```

  - Navigate to a specific directory path:

    ```bash
    cd ~/Documents
    ```

---

## File and Directory Operations

Managing files and directories is fundamental to working effectively in a Linux environment. This section covers essential commands for file and directory operations, ensuring you can navigate, manipulate, and organize your system's file structure efficiently.

### [cat] Command: Viewing File Contents

The `cat` command is straightforward and useful for displaying the contents of a file directly in the terminal.

- **Basic Usage**:

  ```bash
  cat filename
  ```

  Displays the entire contents of `filename` in the terminal.

- **Display Line Numbers**:

  ```bash
  cat -n filename
  ```

  Displays the contents of `filename` with line numbers.

- **Concatenate Multiple Files**:

  ```bash
  cat file1 file2
  ```

  Concatenates `file1` and `file2`, displaying their combined contents.

- **Redirect Output to a New File**:

  ```bash
  cat filename > newfile
  ```

  Redirects the output of `cat` into `newfile`.

### [less] Command: Viewing Large Files

The `less` command allows you to view the contents of a file one screen at a time, which is useful for navigating through large files.

- **Basic Usage**:

  ```bash
  less filename
  ```

  Displays `filename` one screen at a time. Use arrow keys or page up/down to navigate.

- **Search within File**:
  - Press `/` followed by your search term and press `Enter` to search forward.
  - Press `?` followed by your search term and press `Enter` to search backward.

- **Navigate to Line Number**:

  ```bash
  less +n filename
  ```

  Opens `filename` at line `n`.

### [head] and [tail] Commands: Viewing the Beginning and End of Files

The `head` and `tail` commands are used to view the beginning and end of files, respectively.

- **Basic Usage**:

  ```bash
  head filename
  ```

  Displays the first 10 lines of `filename`.

- **Specifying Number of Lines**:

  ```bash
  head -n 20 filename
  ```

  Displays the first 20 lines of `filename`.

- **View End of File**:

  ```bash
  tail filename
  ```

  Displays the last 10 lines of `filename`.

- **Real-time Updates**:

  ```bash
  tail -f filename
  ```

  Displays the last 10 lines of `filename` and continues to output appended data as it comes.

### [grep] Command: Searching for Patterns

The `grep` command is powerful for searching within files based on specified patterns.

- **Basic Usage**:

  ```bash
  grep "pattern" filename
  ```

  Searches for `pattern` in `filename` and displays matching lines.

- **Case Insensitive Search**:

  ```bash
  grep -i "pattern" filename
  ```

  Performs a case-insensitive search for `pattern`.

- **Counting Matches**:

  ```bash
  grep -c "pattern" filename
  ```

  Counts the number of lines containing `pattern` in `filename`.

### [sed] Command: Stream Editor

The `sed` command is useful for performing text transformations on an input stream or file.

- **Basic Usage**:

  ```bash
  sed 's/old_text/new_text/g' filename
  ```

  Replaces `old_text` with `new_text` globally within `filename`.

- **In-place Editing**:

  ```bash
  sed -i 's/old_text/new_text/g' filename
  ```

  Edits `filename` in-place (changes the file directly).

- **Selective Printing**:

  ```bash
  sed -n '5,10p' filename
  ```

  Prints lines 5 to 10 of `filename`.

#### [|] Combining Commands

Linux allows you to combine commands using pipelines (`|`), enabling powerful operations by passing the output of one command as input to another.

- **Example**: Combining `cat` and `grep` to search for a pattern in a file:

  ```bash
  cat filename | grep "pattern"
  ```

- **Example**: Using `cat`, `grep`, and `sed` to search and replace within a file:

  ```bash
  cat filename | grep "pattern" | sed 's/old_text/new_text/g'
  ```

Understanding and mastering these commands will significantly enhance your ability to view, edit, and manipulate files directly from the Linux terminal, improving your productivity and efficiency as a developer.

---

## Understanding the Directory Structure

Understanding the directory structure is crucial for navigating and managing files effectively in a Linux environment. This section provides an overview of essential directories like `/etc` and `/var`, highlighting their purposes and common usage scenarios.

### /etc Directory

The `/etc` directory contains system-wide configuration files and settings. It plays a critical role in configuring various aspects of the operating system and installed applications.

- **Purpose**: Stores configuration files for system services, user accounts, networking, and more.
- **Common Usage**:
  - Editing `/etc/hosts` to manage hostname resolutions.
  - Modifying `/etc/network/interfaces` for network configuration.
  - Configuring `/etc/apt/sources.list` for package repositories.

### /var Directory

The `/var` directory is used to store variable data files that are expected to change frequently during normal system operation.

- **Purpose**: Contains variable data such as logs, databases, mail, and temporary files.
- **Common Usage**:
  - Managing log files in `/var/log`.
  - Storing website content in `/var/www`.
  - Handling mail queues in `/var/mail`.

Understanding these directories and their contents will help you effectively manage system configurations, troubleshoot issues, and ensure smooth operation of your Linux environment.

---

## User Management

Managing user accounts and permissions is essential for maintaining security and controlling access to resources within a Linux system. This section covers basic user management tasks, including creating new users, modifying permissions, and managing file ownership.

### [adduser] Adding a Sudo User

A sudo user is a regular user account with administrative privileges, allowing them to execute commands with superuser (root) permissions when necessary.

- **Objective**: Grant administrative privileges to a user account for performing system-wide tasks.
- **Steps**:
  1. Log in as root or a user with sudo privileges.
  2. Create a new user using the `adduser` command:

     ```bash
     sudo adduser new_username
     ```

  3. Add the user to the sudo group to grant administrative rights:

     ```bash
     sudo usermod -aG sudo new_username
     ```

  4. Verify sudo access by switching to the new user and running a command with `sudo`.

### [passwd] Changing User Passwords

Regularly updating user passwords enhances system security and protects sensitive data from unauthorized access.

- **Objective**: Change the password for a user account.
- **Steps**:
  1. Log in as the user whose password you want to change or as root.
  2. Use the `passwd` command followed by the username to change the password:

     ```bash
     passwd username
     ```

  3. Follow the prompts to enter and confirm the new password.

### [chmod] Modifying User Permissions

Adjusting file and directory permissions ensures users have appropriate access levels to resources based on their roles and responsibilities.

- **Objective**: Modify permissions for files or directories.
- **Steps**:
  - Use the `chmod` command followed by the desired permissions and the file or directory name:

    ```bash
    chmod permissions filename
    ```

  - Example: Grant read, write, and execute permissions to the owner of a file:

    ```bash
    chmod u+rwx filename
    ```

### [chown] Changing File Ownership

The `chown` command changes the owner and group of files or directories.

- **Objective**: Change the owner of a file or directory to the `www-data` user for Apache web server integration.
- **Syntax**:

  ```bash
  sudo chown -R www-data:www-data /var/www/html
  ```

  - `-R`: Recursively changes ownership for all files and directories within `/var/www/html`.
  - `www-data:www-data`: Sets both the owner and group to `www-data`, which is typically used by Apache web server for file and directory access.

Managing user accounts and permissions effectively contributes to a secure and well-organized Linux environment, facilitating collaborative development and system administration tasks.

---

## [scp] Secure Copy

The `scp` command allows secure file transfers between a local and a remote host or between two remote hosts over SSH (Secure Shell). This section covers basic usage and options for `scp`, enabling you to securely copy files between systems.

### Copying Files to a Remote Server

Transferring files to a remote server securely is essential for deploying applications and sharing resources across networks.

- **Objective**: Copy files from the local system to a remote server using `scp`.
- **Syntax**:

  ```bash
  scp local_file username@remote_host:/path/to/destination
  ```

- **Example**:

  ```bash
  scp /local/path/file.txt user@remote.example.com:/home/user/documents/
  ```

  Copies `file.txt` from the local system to `/home/user/documents/` on `remote.example.com`.

### Copying Files from a Remote Server

Retrieve files from a remote server securely using `scp`, ensuring data integrity and confidentiality during file transfers.

- **Objective**: Copy files from a remote server to the local system using `scp`.
- **Syntax**:

  ```bash
  scp username@remote_host:/path/to/source_file /local/path/destination
  ```

- **Example**:

  ```bash
  scp user@remote.example.com:/home/user/documents/file.txt /local/path/
  ```

  Copies `file.txt` from `/home/user/documents/` on `remote.example.com` to `/local/path/` on the local system.

#### [scp] Options

- **Recursive Copy (`-r`)**: Copy entire directories and their contents recursively.

  ```bash
  scp -r local_directory username@remote_host:/path/to/destination
  ```

- **Force Overwrite (`-f`)**: Overwrite existing files at the destination without prompting for confirmation.

  ```bash
  scp -f local_file username@remote_host:/path/to/destination
  ```

Mastering `scp` commands allows seamless file transfers between local and remote systems, facilitating efficient collaboration and deployment processes in our development workflow.

---

## Installing and Configuring a LAMP Stack

A LAMP (Linux, Apache, MySQL, PHP) stack is a popular web development environment. This section guides you through installing and configuring a LAMP stack on your Ubuntu 20.04 system, enabling you to host and develop dynamic websites and web applications locally.

### Installing Apache

Apache is a widely used web server that serves web content over the HTTP protocol.

- **Objective**: Install Apache web server.
- **Steps**:
  1. Update package index:

     ```bash
     sudo apt update
     ```

  2. Install Apache:

     ```bash
     sudo apt install apache2
     ```

  3. Verify Apache installation by accessing http://localhost/ in your web browser.

### Installing MySQL

MySQL is a powerful relational database management system (RDBMS) used for storing and managing data.

- **Objective**: Install MySQL server.
- **Steps**:
  1. Install MySQL server package:

     ```bash
     sudo apt install mysql-server
     ```

  2. Secure MySQL installation and set root password:

     ```bash
     sudo mysql_secure_installation
     ```

  3. Follow the prompts to configure MySQL security options.

### Installing PHP

PHP is a server-side scripting language used for developing dynamic web pages.

- **Objective**: Install PHP and necessary modules.
- **Steps**:
  1. Install PHP and Apache PHP module:

     ```bash
     sudo apt install php libapache2-mod-php
     ```

  2. Verify PHP installation:

     ```bash
     php -v
     ```

  3. Test PHP by creating a `phpinfo.php` file in `/var/www/html/` with the content:

     ```php
     <?php phpinfo(); ?>
     ```

     Access http://localhost/phpinfo.php in your web browser.

### Configuring PHP

Adjust PHP settings based on your development requirements, such as increasing upload file size limits or modifying `php.ini` directives.

- **Objective**: Configure PHP settings for optimal performance.
- **Steps**:
  1. Locate the `php.ini` configuration file:

     ```bash
     sudo nano /etc/php/{version}/apache2/php.ini
     ```

  2. Modify settings as needed (e.g., `upload_max_filesize`, `memory_limit`).
  3. Save and close the file (`Ctrl+X`, `Y`, `Enter`).
  4. Restart Apache for changes to take effect:

     ```bash
     sudo systemctl restart apache2
     ```

Installing and configuring a LAMP stack provides a robust environment for developing and testing web applications locally, empowering you to build dynamic and scalable solutions effectively.

---

## Apache Administration 

Administering Apache involves managing its configuration, virtual hosts, and ensuring smooth operation of your web server. This section covers essential tasks for administering Apache on Ubuntu 20.04, including enabling/disabling sites, adjusting permissions, setting up HTTPS with Certbot, and editing Apache configuration for a WordPress website using Vim.

### Enabling and Disabling Sites

Apache uses virtual hosts to manage multiple websites on a single server. Enabling and disabling sites allows you to control which websites are actively served.

- **Objective**: Enable or disable Apache sites.
- **Steps**:
  1. **Enable a site configuration**:

     ```bash
     sudo a2ensite example.com.conf
     ```

     This command enables the specified site configuration file (`example.com.conf`) and updates Apache's active configuration.

  2. **Disable a site configuration**:

     ```bash
     sudo a2dissite example.com.conf
     ```

     Use this command to disable a site configuration, effectively stopping Apache from serving content for the specified site.

### Configuring Permissions

Adjusting file and directory permissions ensures Apache (`www-data` user) has appropriate access to serve web content securely.

- **Objective**: Set directory permissions for Apache web server.
- **Example**: Grant ownership of web directory to `www-data` user and group:

  ```bash
  sudo chown -R www-data:www-data /var/www/html
  ```

  This command recursively changes ownership of the `/var/www/html` directory and its contents to the `www-data` user and group, allowing Apache to read and write files as needed.

### Setting Up HTTPS with Certbot

Certbot simplifies HTTPS setup by automatically configuring Apache and obtaining SSL/TLS certificates from Let's Encrypt.

- **Objective**: Secure your website with HTTPS using Certbot.
- **Steps**:
  1. **Install Certbot**:

     ```bash
     sudo apt install certbot python3-certbot-apache
     ```

     Ensure Certbot and the Apache plugin are installed to automate SSL/TLS certificate management.

  2. **Obtain a certificate** (replace `example.com` with your domain):

     ```bash
     sudo certbot --apache -d example.com
     ```

     Follow prompts to select domains and configure HTTPS settings. Certbot updates Apache configuration to enable HTTPS.

### Sample Apache Configuration for WordPress Website (Edited via Vim)

Edit Apache configuration files with Vim to customize server settings and virtual hosts for WordPress sites.

- **Objective**: Configure Apache to serve a WordPress website over HTTP and HTTPS.
- **Example Configuration** (`/etc/apache2/sites-available/example.com.conf`):

  ```apache
  <VirtualHost *:80>
      ServerName example.com
      ServerAlias www.example.com
      DocumentRoot /var/www/html

      ErrorLog ${APACHE_LOG_DIR}/error.log
      CustomLog ${APACHE_LOG_DIR}/access.log combined

      <Directory /var/www/html>
          AllowOverride All
      </Directory>
  </VirtualHost>

  ```

  Customize paths and domain names as per your requirements. Ensure SSL/TLS certificates are properly configured for secure HTTPS connections.

### Editing Apache Configuration with Vim

Use Vim to edit Apache configuration files efficiently, ensuring accurate server settings and configurations.

- **Objective**: Edit Apache configuration files for virtual hosts and server settings.
- **Steps**:
  1. **Open configuration file**:

     ```bash
     sudo vim /etc/apache2/sites-available/example.com.conf
     ```

     Replace `example.com.conf` with the actual file name.

  2. **Make changes**:
     Use Vim commands to modify server configurations, virtual hosts, SSL settings, etc.

  3. **Save and exit**:
     Press `Esc`, then type `:wq` and press `Enter` to save changes and exit Vim.

Administering Apache effectively ensures reliable web hosting and performance, supporting seamless deployment and management of web applications in our development environment. Securing your websites with HTTPS using Certbot and customizing Apache configurations with Vim enhances security, functionality, and performance for your web projects.

---

## Monitoring and Logging

Monitoring and logging are crucial aspects of managing a web server environment. This section covers essential tools and practices for monitoring server performance, analyzing logs, and troubleshooting issues effectively on Ubuntu 20.04.

### Server Monitoring with `htop`

`htop` is an interactive process viewer for Unix systems that allows you to monitor system resources in real-time.

- **Objective**: Monitor server resource usage with `htop`.
- **Steps**:
  1. Install `htop`:

     ```bash
     sudo apt install htop
     ```

  2. Run `htop`:

     ```bash
     htop
     ```

     Use `htop` to view CPU, memory, and process information. Press `F1` for help and `F10` to exit.

### Analyzing Apache Logs

Apache logs record server activity, errors, and access attempts, providing valuable insights into website performance and security incidents.

- **Objective**: Analyze Apache logs for troubleshooting and performance monitoring.
- **Log Locations**:
  - Error logs: `/var/log/apache2/error.log`
  - Access logs: `/var/log/apache2/access.log`

  Use `tail` to view the last lines of logs:

  ```bash
  tail -n 50 /var/log/apache2/error.log
  ```

### Monitoring Disk Usage

Monitoring disk usage helps prevent storage issues and ensures optimal server performance.

- **Objective**: Check disk usage and identify large files or directories.
- **Command**:

  ```bash
  du -h --max-depth=1 / | sort -hr
  ```

  This command displays disk usage in human-readable format (`-h`) and sorts results (`sort -hr`) by size in descending order.

### Troubleshooting Apache Issues

Troubleshooting common Apache issues requires identifying errors, checking configurations, and restarting services as needed.

- **Objective**: Resolve Apache-related issues effectively.
- **Steps**:
  1. Check Apache service status:

     ```bash
     sudo systemctl status apache2
     ```

  2. Review error logs for detailed error messages:

     ```bash
     tail -n 50 /var/log/apache2/error.log
     ```

  3. Verify Apache configuration syntax:

     ```bash
     sudo apache2ctl configtest
     ```

  4. Restart Apache service:

     ```bash
     sudo systemctl restart apache2
     ```

### Automating Monitoring with Cron

Cron automates repetitive tasks on Unix-like systems, such as running maintenance scripts and monitoring server metrics.

- **Objective**: Schedule tasks with Cron for automated monitoring.
- **Edit Cron Jobs**:

  ```bash
  crontab -e
  ```

  Add a new Cron job to run a script or command at specified intervals.

Monitoring and logging practices are essential for maintaining server performance, troubleshooting issues promptly, and ensuring the reliability of web applications hosted on Apache. By utilizing tools like `htop`, analyzing logs, monitoring disk usage, and automating tasks with Cron, you can streamline server management and enhance operational efficiency in your development environment.

---

## Backup and Recovery

Ensuring robust backup and recovery mechanisms are essential for maintaining data integrity, minimizing downtime, and safeguarding against data loss in Linux environments. This section explores various tools and strategies to create reliable backups and recover data effectively.

### Backup Tools and Strategies

**Using `tar` for Full Backups**

`tar` (tape archive) is a command-line tool used for archiving files and directories. It's suitable for creating full backups of entire directories or specific files.

**Example:**

```bash
tar -cvf /path/to/backup.tar /path/to/source/
```

- `-c`: Create a new archive.
- `-v`: Verbose mode, display files being archived.
- `-f`: Specify the archive file name.

**Incremental Backups with `rsync`**

`rsync` can be used for incremental backups to synchronize changes since the last backup. It's efficient for minimizing backup time and storage requirements.

**Example:**

```bash
rsync -avz --progress --backup --backup-dir=backup-$(date +%Y%m%d) /path/to/source/ /path/to/backup/
```

- `--backup`: Creates backups of files about to be overwritten or deleted.
- `--backup-dir`: Specifies the directory where backup copies will be stored.

**Database Backup with `mysqldump`**

For backing up MySQL/MariaDB databases, `mysqldump` is the recommended tool. It dumps SQL data to a file, capturing the database structure and content.

**Example:**

```bash
mysqldump -u username -p database_name > /path/to/backup.sql
```

- Replace `username` with your MySQL username and `database_name` with the name of your database.
- `-p`: Prompts for password.

### Backup Strategies

**Full Backup Strategy:**

Perform regular full backups using `tar` to create complete snapshots of critical directories or entire systems. Store these backups securely and ensure they are updated periodically.

**Incremental Backup Strategy:**

Combine `rsync` with a cron job to perform daily incremental backups. This strategy only backs up changes made since the last backup, minimizing storage space and backup time.

**Example Cron Job:**

```bash
0 2 * * * rsync -avz --progress /path/to/source/ /path/to/backup/
```

- This example runs the `rsync` command daily at 2:00 AM.

**Database Backup Strategy:**

Schedule regular database backups using `mysqldump` combined with a cron job to capture database changes. Store backups securely and test restoration procedures periodically to ensure data integrity.

**Example Cron Job for Database Backup:**

```bash
0 3 * * * mysqldump -u username -p database_name > /path/to/backup.sql
```

- This example runs the `mysqldump` command daily at 3:00 AM.

### Recovery Procedures

**Restoring Files from `tar` Backup**

To restore files from a `tar` archive, use the `tar` command with extract (`-x`) option:

```bash
tar -xvf /path/to/backup.tar -C /path/to/restore/
```

**Restoring Files from `rsync` Backup**

Use `rsync` in reverse mode (`--reverse`) to sync data from the backup to the source location for file recovery:

```bash
rsync -av --progress /path/to/backup/ /path/to/restore/
```

**Restoring Database from `mysqldump` Backup**

To restore a MySQL/MariaDB database from a `mysqldump` file, use the `mysql` command:

```bash
mysql -u username -p database_name < /path/to/backup.sql
```

- Replace `username` with your MySQL username and `database_name` with the name of your database.
- `-p`: Prompts for password.

### Best Practices

- **Regular Testing:** Validate backup integrity and restoration procedures regularly to ensure reliability.
- **Offsite Storage:** Store backups in a secure, offsite location or cloud storage for disaster recovery.
- **Documentation:** Maintain detailed documentation of backup schedules, strategies, and configurations for reference during recovery operations.

Backup strategies using tools like `tar`, `rsync`, and `mysqldump`, can effectively safeguard critical data, minimize downtime, and ensure business continuity in Linux environments.

---

## Security Best Practices

Securing your server environment protects against unauthorized access, data breaches, and other security threats. This section covers essential security practices and tools for enhancing server security on Ubuntu 20.04.

### Update and Patch Management

Regularly update system packages and applications to protect against vulnerabilities.

- **Objective**: Implement timely updates and patches.
- **Commands**:

  ```bash
  sudo apt update
  sudo apt upgrade
  ```

### Firewall Configuration with UFW

Use UFW (Uncomplicated Firewall) to manage firewall rules and restrict access to your server.

- **Objective**: Configure firewall rules with UFW.
- **Example**:

  ```bash
  sudo ufw allow ssh
  sudo ufw enable
  ```

### Harden SSH Security

Enhance SSH security by configuring key-based authentication and restricting access.

- **Objective**: Secure SSH access with key-based authentication.
- **Steps**:
  1. Generate SSH key pair:

     ```bash
     ssh-keygen -t rsa -b 4096
     ```

  2. Copy public key to server:

     ```bash
     ssh-copy-id user@server_ip
     ```

### Implementing HTTPS with Certbot

Ensure secure communication by enabling HTTPS with Certbot and Let's Encrypt certificates.

- **Objective**: Secure websites with HTTPS using Certbot.
- **Example**:

  ```bash
  sudo certbot --apache -d example.com
  ```

## Conclusion

Mastering server administration on Ubuntu 20.04 involves understanding key concepts, tools, and best practices for managing web applications and ensuring server security, performance, and reliability. By following this guide, you are equipped with the knowledge and skills to effectively deploy, manage, and secure your development environment, supporting continuous innovation and growth in your organization.

