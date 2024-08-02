# Practical Guide: Setting Up WordPress Using Curl and Other Linux Commands

## Introduction

**Purpose:**
Hey Team! Today, we're diving into a hands-on project to set up a WordPress website using various Linux commands, including `curl`, `unzip`, and others. This exercise is designed to empower you with the skills needed to manage and configure web applications on Linux. Let's roll up our sleeves and get ready to build something awesome!

**Objective:**
Our objective is to successfully download and set up a WordPress website. By the end of this guide, you will have a live WordPress site running on your local development environment, understand the process of configuring Apache, and manage MySQL databases and users.

**Key Learning Outcomes:**

- Master the use of `curl` for downloading files from the internet
- Learn how to unzip files and manage file permissions
- Configure Apache to host a WordPress site
- Create and manage MySQL databases and users
- Update WordPress configuration files and complete the WordPress setup

---

## Let's Get Started!

### Using Curl to Download WordPress

**Curl Command:**
The `curl` command is a powerful tool for transferring data from or to a server. We will use it to download the latest version of WordPress.

**Steps:**
1. Open your terminal.
2. Navigate to the `/var/www` directory where we will host our WordPress site:

    ```bash
    cd /var/www
    ```

3. Download the latest WordPress package using `curl`:

    ```bash
    sudo curl -O https://wordpress.org/latest.zip
    ```

### Unzipping WordPress

**Unzip Command:**
The `unzip` command is used to extract files from a zip archive.

**Steps:**

1. Install the `unzip` package if it's not already installed:

    ```bash
    sudo apt update
    sudo apt install unzip
    ```

2. Unzip the WordPress package:

    ```bash
    sudo unzip latest.zip
    ```

3. Move the extracted files to a new directory called `dev-wp`:

    ```bash
    sudo mv wordpress dev-wp
    ```

4. Set the appropriate permissions for the WordPress files:

    ```bash
    sudo chown -R www-data:www-data /var/www/dev-wp
    ```

### Configuring Apache

**Apache Configuration:**
We need to configure Apache to serve our new WordPress site.

**Steps:**
1. Create a new Apache configuration file for the WordPress site:

    ```bash
    sudo nano /etc/apache2/sites-available/dev-wp.conf
    ```

2. Add the following configuration to the file:

    ```apache
    <VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/dev-wp

        <Directory /var/www/dev-wp>
            Options FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    ```

3. Enable the new site and the rewrite module:

    ```bash
    sudo a2ensite dev-wp.conf
    sudo a2enmod rewrite
    ```

4. Restart Apache to apply the changes:

    ```bash
    sudo systemctl restart apache2
    ```

### Creating MySQL User and Database

**MySQL Commands:**
We'll create a new MySQL user and database for our WordPress site.

**Steps:**

1. Log into MySQL as the root user:

    ```bash
    sudo mysql -u root -p
    ```

2. Create a new database for WordPress:

    ```sql
    CREATE DATABASE dev_wp;
    ```

3. Create a new MySQL user and grant them privileges on the new database:

    ```sql
    CREATE USER 'devuser'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON dev_wp.* TO 'devuser'@'localhost';
    FLUSH PRIVILEGES;
    ```

4. Exit MySQL:

    ```sql
    EXIT;
    ```

### Updating wp-config.php

**WordPress Configuration:**
We need to update the `wp-config.php` file with our database details.

**Steps:**
1. Navigate to the WordPress directory and create a copy of the sample configuration file:

    ```bash
    cd /var/www/dev-wp
    sudo cp wp-config-sample.php wp-config.php
    ```

2. Edit the `wp-config.php` file:

    ```bash
    sudo nano wp-config.php
    ```

3. Update the database settings:

    ```php
    // ** MySQL settings - You can get this info from your web host ** //
    /** The name of the database for WordPress */
    define('DB_NAME', 'dev_wp');

    /** MySQL database username */
    define('DB_USER', 'devuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'password');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    ```

4. Save and close the file.

#### Completing the WordPress Setup

Now that everything is in place, we can complete the WordPress setup through the web browser.

**Steps:**

1. Open your web browser and navigate to `http://localhost`.
2. Follow the on-screen instructions to complete the WordPress installation.
3. Use the database name, username, and password you configured in the `wp-config.php` file.

---

## Summary

Congratulations, Team! You've successfully set up a WordPress site using various Linux commands. This practical guide has equipped you with the skills to manage and configure web applications on Linux. Remember to keep experimenting and exploring new commands and configurations. Together, we'll continue to build amazing projects and grow as a team!
