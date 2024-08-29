# Virtual Users for Email-Only Access

In a multi-domain hosting environment, **virtual users** offer an effective way to manage email accounts without giving users full system access. These users are designed to interact solely with email services, such as Dovecot and Exim, making them an essential tool for securely and efficiently handling multiple domains on a single server.

## What Are Virtual Users?

**Virtual users** are user accounts that exist solely for accessing specific services, like email. Unlike system users, virtual users do not have a shell or home directory and are managed separately from the system’s user base.

**Key Characteristics:**

- **Service-Specific Accounts:** Virtual users are associated only with the services they need, such as email, and have no broader system presence.
- **No Shell Access:** These users cannot log in to the server via SSH or any other terminal service, ensuring that they are isolated from the core system.
- **Isolated Management:** Virtual users are typically managed through configuration files or a database, separate from system user accounts.

**Advantages:**

- **Enhanced Security:** Virtual users are isolated from the system, reducing the risk of unauthorized access.
- **Resource Efficiency:** Virtual users consume fewer resources because they don’t require a home directory or shell.

## Setting Up Virtual Users for Email

### Using a Flat File for Virtual User Management

A common and straightforward method for managing virtual users is to store their credentials in a flat file, similar to the system’s `/etc/passwd` file. This method is particularly useful for small to medium-sized setups and provides a clear and manageable way to handle multiple email accounts.

**Step 1: Creating the Virtual User File**

Start by creating a file, for example, `/etc/mail/virtual_users`, where you will store the virtual users' credentials and mail directory information.

```plaintext
user1@domain.com:{SHA512-CRYPT}$6$random-salt$hash-of-password:maildir:/var/mail/virtual/domain.com/user1/
user2@domain.com:{SHA512-CRYPT}$6$random-salt$hash-of-password:maildir:/var/mail/virtual/domain.com/user2/
```

- **Email Address:** The virtual user’s email address.
- **Encrypted Password:** The password is securely hashed, typically using `SHA512-CRYPT`. You can generate this hash using `doveadm pw -s SHA512-CRYPT`.
- **Mail Directory:** Specifies where the user’s emails will be stored, such as `/var/mail/virtual/domain.com/user1/`.

**Step 2: Configuring Dovecot for Virtual Users**

Next, configure Dovecot to authenticate and manage these virtual users based on the flat file you’ve created.

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

- **`passdb`:** Defines how Dovecot reads and authenticates virtual users. It uses the `passwd-file` driver to reference the `virtual_users` file.
- **`userdb`:** Maps virtual users to their mail directories with correct permissions, ensuring that emails are stored securely.

**Step 3: Configuring Exim4 for Email Delivery**

Finally, configure Exim4 to ensure that incoming emails are delivered to the correct mail directories for each virtual user.

```plaintext
virtual_aliases:
  driver = redirect
  domains = dsearch;/etc/mail/domains
  data = /var/mail/virtual/${domain}/${local_part}/
```

- **Domains:** Specifies the domains that are being managed by Exim4.
- **Data:** Determines where Exim4 should deliver each user’s email, using the domain and local part (the username) to identify the correct mail directory.

---

### **Summary of Virtual User Setup**

- **File Location:** Store virtual user credentials in a flat file, such as `/etc/mail/virtual_users`.
- **Dovecot Configuration:** Use `passwd-file` for authentication and `static` userdb for mapping mail directories.
- **Exim4 Configuration:** Deliver emails based on the domain and local part, ensuring correct placement in user-specific mail directories.

---
