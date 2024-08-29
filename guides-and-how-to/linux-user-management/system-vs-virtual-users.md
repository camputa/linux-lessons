# System Users vs. Virtual Users

When managing a Linux server in a multi-domain hosting environment, it’s important to differentiate between **system users** and **virtual users**. Each type of user serves a distinct purpose and is managed differently depending on the services provided, such as SSH access or email hosting.

## System Users

**System users** are the traditional user accounts created directly on the Linux operating system. These users have their own unique User ID (UID), a home directory, and usually, shell access. System users are typically used for individuals who need direct access to the server, such as administrators or developers.

### Creating System Users with `useradd`

The `useradd` command is used to create new system users. This command offers several options to customize the user account:

- **`-m`**: This option creates a home directory for the user at `/home/username`.
- **`-s`**: Specifies the login shell for the user, such as `/bin/bash` for the Bash shell.
- **`-G`**: Adds the user to one or more groups.
- **`-d`**: Allows you to specify a different home directory.

**Example Command:**

```bash
sudo useradd -m -s /bin/bash -G sudo username
sudo passwd username
```

This command creates a new user with a home directory, assigns the Bash shell, and adds the user to the `sudo` group, giving them administrative privileges. The `passwd` command is then used to set the user’s password.

### System Users' Characteristics

- **Home Directory:** Each user has a dedicated directory where personal files, settings, and configurations are stored.
- **Shell Access:** System users can log into the server via SSH or directly from the terminal, giving them the ability to execute commands and manage the system.
- **File Permissions:** Linux file permissions (read, write, execute) apply to system users, allowing detailed control over who can access and modify files.

**Common Use Cases:**

- **Administrators:** For managing server configurations, updates, and security settings.
- **Developers:** For deploying and managing applications, accessing logs, and performing development tasks.

**Advantages:**

- Full access to server resources and services.
- Highly configurable for individual user needs.

**Disadvantages:**

- Higher security risk if not managed properly.
- Increased resource usage per user.

## Virtual Users

**Virtual users** are accounts created for specific services, such as email, without giving them full system access. Unlike system users, virtual users do not have a shell or home directory on the server. They are typically managed through service-specific configurations and are ideal for multi-domain hosting environments where you need to create numerous user accounts, especially for email services.

### Using Flat Files for Virtual Users with Exim and Dovecot

In many hosting setups, virtual users for email services are managed using flat files, such as a custom `passwd`-like file. This method is simpler and often more efficient than using a database, especially for smaller setups.

**Example Configuration:**

1. **Create the Virtual User File:**
   
   You can create a file, for example, `/etc/mail/virtual_users`, to store virtual user credentials.

   ```plaintext
   user@domain.com:{SHA512-CRYPT}$6$random-salt$hash-of-password:maildir:/var/mail/virtual/user/domain.com/
   ```

   - The format typically includes the email address, encrypted password, and the mail directory.
   - Passwords can be encrypted using tools like `doveadm pw -s SHA512-CRYPT` to generate a secure hash.

2. **Configure Dovecot:**

   Update Dovecot’s configuration to recognize this virtual user file:

   ```plaintext
   passdb {
     driver = passwd-file
     args = /etc/mail/virtual_users
   }

   userdb {
     driver = static
     args = uid=vmail gid=vmail home=/var/mail/virtual/%d/%n
   }
   ```

   - **`passdb`**: Configures how Dovecot reads the user credentials.
   - **`userdb`**: Defines how Dovecot maps virtual users to directories and sets permissions.

3. **Configure Exim4:**

   Update Exim4 to deliver emails to the virtual users’ mail directories:

   ```plaintext
   virtual_aliases:
     driver = redirect
     domains = dsearch;/etc/mail/domains
     data = /var/mail/virtual/${domain}/${local_part}/
   ```

   - Exim4 reads the `virtual_users` file to determine where to deliver incoming mail for each virtual user.

### Virtual Users' Characteristics

- **No Shell Access:** Virtual users cannot log into the server directly and are limited to accessing only the services they are configured for (e.g., email).
- **Service-Specific Configuration:** Virtual users are typically managed via configuration files or databases specific to the service, like Exim4 or Dovecot.
- **Resource Efficiency:** Virtual users consume fewer resources, making them suitable for large-scale email hosting across multiple domains.

**Common Use Cases:**

- **Email Accounts:** Creating and managing email addresses for multiple domains without giving users direct server access.
- **Web Application Users:** Managing users for web applications where backend server access is unnecessary.

**Advantages:**

- **Security:** Virtual users are isolated from the system, minimizing security risks.
- **Scalability:** Easily scalable to handle hundreds or thousands of users across multiple domains.

**Disadvantages:**

- **Limited Functionality:** Restricted to specific services without broader server access.
- **Complex Management:** Requires proper configuration and management, often involving multiple files or databases.

---
