# Practical Guide: Mastering MySQL Commands on Linux

Hey Team! Today, we're diving into the world of MySQL, a powerful relational database management system that is crucial for our projects. Understanding MySQL commands will empower you to manage databases efficiently and securely. Let’s get ready to enhance our database skills and take control of our data!

Our objective is to get comfortable using MySQL commands on Linux, including setting up MySQL to listen on a different port and resetting the root password. By mastering these commands, you'll be equipped to handle database management tasks with confidence and precision.

**Key Learning Outcomes:**
- Gain a solid understanding of essential MySQL commands and their options
- Learn how to configure MySQL to listen on a different port
- Understand the process of resetting the MySQL root password
- Develop the ability to troubleshoot and verify MySQL configurations

---

## Let's Get Started!

### 1. Understanding MySQL Commands

MySQL commands are used to interact with the MySQL server, allowing you to manage databases, users, and permissions. These commands can be executed from the MySQL shell or directly from the Linux terminal.

**Common MySQL Commands:**
- `mysql -u username -p`: Log into MySQL with a specific user.
- `SHOW DATABASES;`: List all databases on the MySQL server.
- `USE database_name;`: Select a database to work with.
- `SHOW TABLES;`: List all tables in the selected database.
- `CREATE DATABASE database_name;`: Create a new database.
- `CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';`: Create a new MySQL user.
- `GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'localhost';`: Grant user privileges.
- `FLUSH PRIVILEGES;`: Reload the privileges tables in MySQL.
- `EXIT;`: Exit the MySQL shell.

### 2. Installing MySQL on Ubuntu

Before we can use MySQL commands, we need to install MySQL on our Ubuntu system.

**Steps:**
1. Update package information:

    ```bash
    sudo apt update
    ```

2. Install MySQL server:

    ```bash
    sudo apt install mysql-server
    ```

3. Start MySQL service:

    ```bash
    sudo systemctl start mysql
    ```

4. Enable MySQL to start on boot:

    ```bash
    sudo systemctl enable mysql
    ```

### 3. Configuring MySQL to Listen on a Different Port

By default, MySQL listens on port 3306. However, there may be scenarios where you need to change this port.

**Steps:**
1. Open the MySQL configuration file:

    ```bash
    sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
    ```

2. Locate the line that begins with `port` and change the port number to your desired value, for example:

    ```ini
    port = 3307
    ```

3. Save and exit the text editor.

4. Restart MySQL to apply the changes:

    ```bash
    sudo systemctl restart mysql
    ```

5. Verify MySQL is listening on the new port:

    ```bash
    sudo netstat -tulnp | grep mysql
    ```

### 4. Resetting the MySQL Root Password

If you ever forget the root password, you can reset it using the following steps.

**Steps:**
1. Stop the MySQL service:

    ```bash
    sudo systemctl stop mysql
    ```

2. Start MySQL in safe mode with the `--skip-grant-tables` option:

    ```bash
    sudo mysqld_safe --skip-grant-tables &
    ```

3. Log into MySQL without a password:

    ```bash
    mysql -u root
    ```

4. Once logged in, change the root password:

    ```sql
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'new_password';
    FLUSH PRIVILEGES;
    ```

5. Exit MySQL:

    ```sql
    EXIT;
    ```

6. Stop MySQL safe mode:

    ```bash
    sudo mysqladmin shutdown
    ```

7. Start the MySQL service:

    ```bash
    sudo systemctl start mysql
    ```

## Practice Tutorial: Managing MySQL on Linux

**Objective:** Practice using MySQL commands, changing the listening port, and resetting the root password.

1. **Install MySQL:**
    - Update and install MySQL server:

      ```bash
      sudo apt update
      sudo apt install mysql-server
      ```

2. **Change MySQL Listening Port:**
    - Edit the configuration file to change the port:

      ```bash
      sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
      ```

    - Change `port` to `3307` and save the file.
    - Restart MySQL:

      ```bash
      sudo systemctl restart mysql
      ```

3. **Reset Root Password:**
    - Stop MySQL service:

      ```bash
      sudo systemctl stop mysql
      ```

    - Start MySQL in safe mode:

      ```bash
      sudo mysqld_safe --skip-grant-tables &
      ```

    - Log into MySQL and change the root password:

      ```bash
      mysql -u root
      ```

      ```sql
      ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'new_password';
      FLUSH PRIVILEGES;
      ```

    - Stop MySQL safe mode:

      ```bash
      sudo mysqladmin shutdown
      ```

    - Start MySQL service:

      ```bash
      sudo systemctl start mysql
      ```

---

## Summary

Fantastic work, team! You've now got the skills to manage MySQL on Linux, including changing the listening port and resetting the root password. These essential commands and configurations will empower you to handle our databases with expertise and confidence.

Remember, MySQL is a vital part of our infrastructure, and your ability to manage it effectively ensures the stability and security of our data. Keep experimenting, stay curious, and continue to build on these foundational skills. Together, we'll keep driving our projects forward with precision and excellence!
