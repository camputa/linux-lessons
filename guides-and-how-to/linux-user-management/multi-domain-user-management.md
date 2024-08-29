# Multi-Domain User Management

Managing users across multiple domains on a single server requires careful planning and organization. In a multi-domain hosting environment, you need to ensure that each domain's users are properly isolated, secure, and managed efficiently. This section will cover the best practices, configurations, and tools necessary to manage system and virtual users across multiple domains.

## 1. Overview of Multi-Domain User Management

When hosting multiple domains on a single server, each domain may have its own set of users, who require different levels of access. These users can range from system users with shell access to virtual users who only need email access. Proper management ensures that users are correctly segregated by domain, reducing the risk of cross-domain security issues and simplifying administration.

Key considerations include:

- **User Isolation:** Ensuring that users from different domains cannot interfere with each other’s data or services.
- **Resource Allocation:** Managing resources like disk space and memory, ensuring fair distribution across domains.
- **Scalability:** Preparing the system to easily add or remove domains and users as needed.

## 2. System Users Across Multiple Domains

**Purpose:** System users typically require shell access to the server, often for tasks like managing websites, databases, or performing maintenance. In a multi-domain setup, system users must be carefully managed to ensure they can only access resources relevant to their domain.

**User Isolation:**

- **Home Directories:** Ensure that each system user has a separate home directory, typically under `/home/username`, which is isolated from other users.

  **Example Command:**

  ```bash
  useradd -m -s /bin/bash username
  ```

  - **`-m`**: Creates a home directory for the user.
  - **`-s /bin/bash`**: Specifies the user's shell, in this case, Bash.

- **File Permissions:** Set appropriate permissions on each user’s home directory to prevent unauthorized access from other users.

  **Example Command:**

  ```bash
  chmod 700 /home/username
  ```

  - **`chmod 700`**: Grants full access to the user and denies access to others.

**Resource Quotas:**

- **Disk Quotas:** Implement disk quotas to prevent any one user from consuming excessive disk space, which is crucial in a multi-domain environment where resources are shared.

  **Example Command:**

  ```bash
  edquota -u username
  ```

  This command allows you to set disk quotas for the specified user.

- **CPU and Memory Limits:** Use tools like `cgroups` or `systemd` to limit the CPU and memory usage of system users.

## 3. Virtual Users for Email Across Multiple Domains

**Purpose:** Virtual users are typically used for email-only access. They don’t have shell access to the server, and their data is stored in virtual mailboxes. In a multi-domain setup, each domain can have its own set of virtual email users, isolated from other domains.

**Virtual User Isolation:**

- **Directory Structure:** Organize virtual users' mail directories under `/var/mail/virtual/domain.com/username`. This structure ensures that each domain’s users are neatly segregated.

  **Example Directory Structure:**

  ```
  /var/mail/virtual/
  ├── domain1.com/
  │   ├── user1/
  │   └── user2/
  ├── domain2.com/
  │   ├── user1/
  │   └── user2/
  ```

  Each user’s mail is stored under their respective domain directory, ensuring clear separation.

- **File Ownership and Permissions:** Set the appropriate ownership and permissions on mail directories to ensure only the mail service can access them.

  **Example Commands:**

  ```bash
  chown -R vmail:vmail /var/mail/virtual/
  chmod -R 700 /var/mail/virtual/
  ```

**Flat File Management:**

- **Virtual Users File:** Use a flat file (e.g., `/etc/mail/virtual_users`) to manage virtual users for each domain. This file maps email addresses to their encrypted passwords and mail directories.

  **Example Entry in `virtual_users`:**

  ```plaintext
  user1@domain1.com:$6$rounds=5000$encryptedpassword:/var/mail/virtual/domain1.com/user1/
  user2@domain2.com:$6$rounds=5000$encryptedpassword:/var/mail/virtual/domain2.com/user2/
  ```

- **Secure Storage:** Ensure the `virtual_users` file is securely stored and only accessible by the mail server.

  **Example Command:**

  ```bash
  chmod 600 /etc/mail/virtual_users
  ```

  - **`chmod 600`**: Allows read and write access only to the owner, typically the mail service.

**Email Server Configuration:**

- **Dovecot Configuration:** Configure Dovecot to use the `virtual_users` file for authentication, ensuring that users can only access their own mail.

  **Example Configuration:**

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

  - **`%d`**: Domain part of the email.
  - **`%n`**: Username part of the email.

- **Exim Configuration:** Configure Exim to route incoming mail to the correct virtual user’s mailbox based on the domain.

  **Example Configuration:**

  ```plaintext
  virtual_aliases:
    driver = redirect
    domains = dsearch;/etc/mail/virtual_domains
    data = ${lookup{$local_part@$domain}lsearch{/etc/mail/virtual_users}}
    no_more
  ```

## 4. Managing User Data Across Domains

**Backup and Recovery:**

- **Domain-Level Backups:** Implement domain-level backups to ensure that each domain’s data can be restored independently. This is particularly important in a multi-domain environment where different clients may require different backup schedules or retention policies.

  **Example Command:**

  ```bash
  tar -czf /backup/domain1.com.tar.gz /var/mail/virtual/domain1.com/
  ```

  This command creates a compressed archive of all mail for `domain1.com`.

- **Testing Restores:** Regularly test your backup and recovery process to ensure that user data can be restored quickly in case of an incident.

**Monitoring and Alerts:**

- **Domain-Specific Monitoring:** Set up monitoring for each domain to track metrics such as disk usage, mail queue length, and login attempts. This allows you to detect issues before they affect the users.

- **Alerts:** Configure alerts for specific events, such as when a domain’s disk usage exceeds a certain threshold or when there are multiple failed login attempts for a particular user.

  **Example Command:**

  ```bash
  df -h /var/mail/virtual/ | mail -s "Disk Usage Alert" admin@example.com
  ```

  This sends an email alert if disk usage for virtual mail directories exceeds a certain level.

## 5. Security Considerations

**Isolating Domains:** 

- **Chroot Jails:** Consider using chroot jails to isolate system users further, especially if they have access to potentially sensitive data or if you want to add an additional layer of security.
  
- **Separate Databases:** For virtual users, consider using separate databases or tables for each domain, ensuring that a compromise in one domain doesn’t affect others.

**Regular Audits:**

- **Audit Permissions:** Regularly audit file permissions, user access levels, and configurations to ensure that no unauthorized access is possible.
  
  **Example Command:**

  ```bash
  find /var/mail/virtual/ -type d -exec chmod 700 {} \;
  ```

  This command ensures that all mail directories have the correct permissions set.

---
