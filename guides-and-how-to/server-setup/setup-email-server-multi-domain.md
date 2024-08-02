# Comprehensive Wiki: Secure Email Server Setup with Postfix, Dovecot, and Roundcube on Ubuntu 22.04

## Introduction

This guide provides detailed step-by-step instructions to set up a secure email server using Postfix, Dovecot, and Roundcube on Ubuntu 22.04. The example includes configurations for three domains (domain1.com, domain2.com, domain3.com) with two users each (user1, user2). By the end of this guide, you'll have a fully functional, secure email server with webmail access.

## Prerequisites

- A fresh installation of Ubuntu 22.04.
- Root or sudo access.
- Basic understanding of Linux command line operations.
- DNS records configured for your domains.

## Step 1: Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```
- **Explanation**: Ensures that all system packages are up-to-date and secure.

## Step 2: Install Postfix

### Install Postfix

```bash
sudo apt install postfix -y
```
- **Explanation**: Installs Postfix, a popular and flexible mail transfer agent (MTA).

### Basic Postfix Configuration

During the installation, you'll be prompted to configure Postfix. Select "Internet Site" and enter the primary domain name (e.g., domain1.com).

### Postfix Main Configuration

```bash
sudo nano /etc/postfix/main.cf
```

Add or update the following settings:

```plaintext
myhostname = mail.domain1.com
mydomain = domain1.com
myorigin = /etc/mailname
inet_interfaces = all
inet_protocols = ipv4
mydestination = $myhostname, localhost.$mydomain, localhost
virtual_alias_domains =
virtual_alias_maps = hash:/etc/postfix/virtual
virtual_mailbox_domains = hash:/etc/postfix/vhosts
virtual_mailbox_base = /var/mail/vhosts
virtual_mailbox_maps = hash:/etc/postfix/vmailbox
virtual_minimum_uid = 100
virtual_uid_maps = static:5000
virtual_gid_maps = static:5000
smtpd_sasl_auth_enable = yes
smtpd_sasl_security_options = noanonymous
smtpd_sasl_local_domain = $mydomain
broken_sasl_auth_clients = yes
smtpd_recipient_restrictions = permit_sasl_authenticated,permit_mynetworks,reject_unauth_destination
smtpd_use_tls = yes
smtpd_tls_cert_file=/etc/letsencrypt/live/mail.domain1.com/fullchain.pem
smtpd_tls_key_file=/etc/letsencrypt/live/mail.domain1.com/privkey.pem
smtpd_tls_session_cache_database = btree:${data_directory}/smtpd_scache
smtp_tls_session_cache_database = btree:${data_directory}/smtp_scache
```
- **Explanation**: Configures Postfix to handle emails for virtual domains and users, enabling SSL/TLS for secure communication.

### Configure Virtual Domains and Users

1. **Create the virtual domains file**:
    ```bash
    sudo nano /etc/postfix/vhosts
    ```
    Add the following content:
    ```plaintext
    domain1.com    OK
    domain2.com    OK
    domain3.com    OK
    ```

2. **Create the virtual mailboxes file**:
    ```bash
    sudo nano /etc/postfix/vmailbox
    ```
    Add the following content:
    ```plaintext
    user1@domain1.com    domain1.com/user1/
    user2@domain1.com    domain1.com/user2/
    user1@domain2.com    domain2.com/user1/
    user2@domain2.com    domain2.com/user2/
    user1@domain3.com    domain3.com/user1/
    user2@domain3.com    domain3.com/user2/
    ```

3. **Create the virtual aliases file**:
    ```bash
    sudo nano /etc/postfix/virtual
    ```
    Add the following content:
    ```plaintext
    postmaster@domain1.com    user1@domain1.com
    postmaster@domain2.com    user1@domain2.com
    postmaster@domain3.com    user1@domain3.com
    ```

4. **Create necessary directories**:
    ```bash
    sudo mkdir -p /var/mail/vhosts/domain1.com/user1
    sudo mkdir -p /var/mail/vhosts/domain1.com/user2
    sudo mkdir -p /var/mail/vhosts/domain2.com/user1
    sudo mkdir -p /var/mail/vhosts/domain2.com/user2
    sudo mkdir -p /var/mail/vhosts/domain3.com/user1
    sudo mkdir -p /var/mail/vhosts/domain3.com/user2
    ```

5. **Update the postfix maps**:
    ```bash
    sudo postmap /etc/postfix/vhosts
    sudo postmap /etc/postfix/vmailbox
    sudo postmap /etc/postfix/virtual
    ```

6. **Reload Postfix**:
    ```bash
    sudo systemctl reload postfix
    ```

## Step 3: Install Dovecot

### Install Dovecot

```bash
sudo apt install dovecot-core dovecot-imapd dovecot-pop3d -y
```
- **Explanation**: Installs Dovecot and its IMAP and POP3 modules.

### Dovecot Configuration

1. **Edit main Dovecot configuration**:
    ```bash
    sudo nano /etc/dovecot/dovecot.conf
    ```
    Add or update the following:
    ```plaintext
    protocols = imap pop3 lmtp
    mail_location = maildir:/var/mail/vhosts/%d/%n
    mail_privileged_group = mail
    ```

2. **Configure Authentication**:
    ```bash
    sudo nano /etc/dovecot/conf.d/10-auth.conf
    ```
    Add or update the following:
    ```plaintext
    disable_plaintext_auth = yes
    auth_mechanisms = plain login
    passdb {
      driver = passwd-file
      args = /etc/dovecot/users
    }
    userdb {
      driver = static
      args = uid=vmail gid=vmail home=/var/mail/vhosts/%d/%n
    }
    ```

3. **Create Virtual User Password File**:
    ```bash
    sudo nano /etc/dovecot/users
    ```
    Add users with encrypted passwords:
    ```plaintext
    user1@domain1.com:{SHA512-CRYPT}$6$2rOs9z24$FgTVmNTP8k3F3vL2p.mzLsB2j21/2UFGnb7oYgX.F5eJCR4bPo68TiIjIfkF4yU5YBti14YxOnPrXq.jbbLbP0
    user2@domain1.com:{SHA512-CRYPT}$6$aGZ7uP3y$xN5q9kXfW5d8La1jqsmMwMzRVnP2z3Nm.e/VlePqU7sOEC7X7Lwpe3Lf9GTB72avA0gNO1cbsfZSmABKKHFs1
    user1@domain2.com:{SHA512-CRYPT}$6$ZmZXp19u$f4aSxZDz9aF5UjJLNSyJmS0FnD0VrKr/kJHgF0qg4z3qF9F/Qeq21L8i3D1IoDP7Aq4iF0KjXx7b8F0E/aFrO1
    user2@domain2.com:{SHA512-CRYPT}$6$T0xXlX1B$M2Q6GRrQh37DxRhCPOg8Oevs1frZ8w1EtO7Bb4a7Y9nPZFA9JbF.JQL4gL8XThtQjq9jbsSzLw9/zSt2z5GcU/
    user1@domain3.com:{SHA512-CRYPT}$6$Slk4jP1n$QbBx5J1Fb5k8QK6FJk3wU5A3QlTp68QZ6T4SjBqlH9cGg9x5Q9P0G8q1V4d8J2J8Gp9jN6S2L8QjF0l7X4r5n1
    user2@domain3.com:{SHA512-CRYPT}$6$X8T7fN1z$WbLrQF3pHkF8l3N6Rm9eO6JbB8XhN3F5LsWlF6kU8TqP7D8S3U7nW8L4J7T6F3J2Gm1kR8N4Q7lL4N1Q8f4m0
    ```

4. **Set Permissions**:
    ```bash
    sudo chmod 600 /etc/dovecot/users
    sudo chown -R vmail:vmail /var/mail/vhosts
    ```

5. **Edit Dovecot Master Configuration**:
    ```bash
    sudo nano /etc/dovecot/conf.d/10-master.conf
    ```
    Add the following:
    ```plaintext
    service auth {
      unix_listener /var/spool/postfix/private/auth {
        mode = 0666


        user = postfix
        group = postfix
      }
    }
    ```

6. **Restart Dovecot**:
    ```bash
    sudo systemctl restart dovecot
    ```

## Step 4: Install Roundcube

### Install Apache, PHP, and Required Modules

```bash
sudo apt install apache2 php php-mysql libapache2-mod-php php-intl php-json php-common php-mbstring php-xml php-gd php-curl php-zip -y
```
- **Explanation**: Installs Apache web server, PHP, and necessary PHP modules.

### Download and Configure Roundcube

1. **Download Roundcube**:
    ```bash
    wget https://github.com/roundcube/roundcubemail/releases/download/1.5.0/roundcubemail-1.5.0-complete.tar.gz
    tar xvf roundcubemail-1.5.0-complete.tar.gz
    sudo mv roundcubemail-1.5.0 /var/www/html/roundcube
    ```

2. **Configure Apache for Roundcube**:
    ```bash
    sudo nano /etc/apache2/sites-available/roundcube.conf
    ```

    Add the following:
    ```plaintext
    <VirtualHost *:80>
        ServerAdmin admin@domain1.com
        DocumentRoot /var/www/html/roundcube

        <Directory /var/www/html/roundcube/>
            Options +FollowSymlinks
            AllowOverride All
            <IfModule mod_dav.c>
                Dav off
            </IfModule>
            SetEnv HOME /var/www/html/roundcube
            SetEnv HTTP_HOME /var/www/html/roundcube
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/roundcube_error.log
        CustomLog ${APACHE_LOG_DIR}/roundcube_access.log combined
    </VirtualHost>
    ```

3. **Enable Roundcube Site and Apache Modules**:
    ```bash
    sudo a2ensite roundcube.conf
    sudo a2enmod rewrite
    sudo systemctl restart apache2
    ```

4. **Setup Roundcube Database**:
    ```bash
    sudo mysql -u root -p
    ```

    Execute the following SQL commands:
    ```sql
    CREATE DATABASE roundcube;
    GRANT ALL PRIVILEGES ON roundcube.* TO 'roundcubeuser'@'localhost' IDENTIFIED BY 'password';
    FLUSH PRIVILEGES;
    ```

5. **Configure Roundcube**:
    Navigate to `http://your-server-ip/roundcube/installer` and follow the installation wizard to complete the configuration.

### Configure Roundcube to Use Postfix and Dovecot

1. **Edit Roundcube Configuration**:
    ```bash
    sudo nano /var/www/html/roundcube/config/config.inc.php
    ```

2. **Add Mail Server Settings**:
    ```php
    $config['default_host'] = 'ssl://mail.domain1.com';
    $config['default_port'] = 993;
    $config['smtp_server'] = 'tls://mail.domain1.com';
    $config['smtp_port'] = 587;
    $config['smtp_user'] = '%u';
    $config['smtp_pass'] = '%p';
    ```

3. **Finalize and Secure Roundcube**:
    ```bash
    sudo chown -R www-data:www-data /var/www/html/roundcube
    sudo systemctl restart apache2
    ```

## Conclusion

By following these detailed steps, you have successfully set up a secure email server using Postfix, Dovecot, and Roundcube on Ubuntu 22.04. This configuration supports multiple domains and virtual users, providing a secure and robust email solution with webmail access.