# Troubleshooting and Common Issues

Managing users on a Linux server, especially in a multi-domain hosting environment, can sometimes lead to unexpected issues. This section outlines common user management problems, their potential causes, and step-by-step troubleshooting methods to help you resolve these issues efficiently. By understanding these common pitfalls, you can quickly identify and fix problems, ensuring smooth server operations.

## Common Issues with System Users

### **Issue 1: Unable to Log in to the Server**

**Symptoms:** A user reports being unable to log in via SSH or the console.

**Possible Causes:**

- Incorrect username or password.
- The user's shell is set to `/bin/false` or `/usr/sbin/nologin`.
- Account is locked or expired.
- Incorrect SSH key permissions.

**Troubleshooting Steps:**

1. **Verify Username and Password:**

   Ensure the user is entering the correct credentials. You can check the username in the `/etc/passwd` file:

   ```bash
   grep username /etc/passwd
   ```

2. **Check Shell Settings:**

   Verify that the user’s shell is set correctly:

   ```bash
   grep username /etc/passwd
   ```

   Look for the shell assigned to the user at the end of the line. It should be `/bin/bash` or another valid shell, not `/bin/false` or `/usr/sbin/nologin`.

   **Example Output:**

   ```plaintext
   username:x:1001:1001::/home/username:/bin/bash
   ```

3. **Check Account Status:**

   Determine if the account is locked or expired:

   ```bash
   passwd -S username
   ```

   - **`L`** indicates the account is locked.
   - **`E`** indicates the account is expired.

   Unlock or extend the account if necessary:

   ```bash
   passwd -u username  # Unlocks the account
   chage -E -1 username  # Removes expiration
   ```

4. **Verify SSH Key Permissions:**

   If using SSH keys, check the permissions on the `.ssh` directory and `authorized_keys` file:

   ```bash
   ls -ld /home/username/.ssh
   ls -l /home/username/.ssh/authorized_keys
   ```

   The `.ssh` directory should have `700` permissions, and `authorized_keys` should have `600` permissions.

   ```bash
   chmod 700 /home/username/.ssh
   chmod 600 /home/username/.ssh/authorized_keys
   ```

### **Issue 2: Permissions Denied When Accessing Files**

**Symptoms:** A user cannot access files or directories, receiving "Permission denied" errors.

**Possible Causes:**

- Incorrect file or directory ownership.
- Incorrect file or directory permissions.
- SELinux or AppArmor restrictions.

**Troubleshooting Steps:**

1. **Check Ownership:**

   Verify that the user owns the files or directories they are trying to access:

   ```bash
   ls -l /path/to/file_or_directory
   ```

   If ownership is incorrect, change it with:

   ```bash
   chown username:groupname /path/to/file_or_directory
   ```

2. **Check Permissions:**

   Ensure the correct permissions are set on the file or directory:

   ```bash
   ls -l /path/to/file_or_directory
   ```

   Adjust permissions as needed:

   ```bash
   chmod 755 /path/to/directory  # For directories
   chmod 644 /path/to/file       # For files
   ```

3. **Check SELinux or AppArmor:**

   If SELinux or AppArmor is enabled, it might be restricting access. Use the following command to check the SELinux status:

   ```bash
   sestatus
   ```

   If SELinux is enforcing and causing the issue, consider adjusting the SELinux policy or temporarily setting it to permissive mode:

   ```bash
   setenforce 0  # Sets SELinux to permissive mode
   ```

   For AppArmor, use:

   ```bash
   aa-status
   ```

   If AppArmor is causing the issue, you may need to adjust the profile or disable it for the specific application.

## Common Issues with Virtual Users

### **Issue 3: Virtual Users Unable to Receive Email**

**Symptoms:** Emails sent to virtual users bounce back, or the users do not receive them.

**Possible Causes:**

- Incorrect virtual user configuration.
- Issues with mail directory permissions.
- Problems with email server configuration (e.g., Exim, Dovecot).

**Troubleshooting Steps:**

1. **Check Virtual User Configuration:**

   Ensure the virtual user is correctly configured in the flat file (e.g., `/etc/mail/virtual_users`):

   ```bash
   grep user@domain.com /etc/mail/virtual_users
   ```

   Ensure the user’s entry is correct and points to the right directory.

2. **Verify Mail Directory Permissions:**

   Check the ownership and permissions of the virtual user's mail directory:

   ```bash
   ls -ld /var/mail/virtual/domain.com/user
   ```

   Set the correct ownership and permissions:

   ```bash
   chown -R vmail:vmail /var/mail/virtual/domain.com/user
   chmod -R 700 /var/mail/virtual/domain.com/user
   ```

3. **Check Email Server Logs:**

   Review the logs for your mail server (Exim, Dovecot) to identify errors:

   **Exim Log:**

   ```bash
   tail -f /var/log/exim4/mainlog
   ```

   **Dovecot Log:**

   ```bash
   tail -f /var/log/dovecot.log
   ```

   Look for any specific errors or warnings related to the virtual user.

### **Issue 4: Virtual Users Unable to Authenticate**

**Symptoms:** A virtual user is unable to log in to the email service, receiving authentication errors.

**Possible Causes:**

- Incorrect password or hash in the virtual users file.
- Issues with the authentication service configuration.
- Permission issues on the authentication file.

**Troubleshooting Steps:**

1. **Check Password Hash:**

   Verify that the password hash in the virtual users file is correct and matches the user’s password:

   ```bash
   grep user@domain.com /etc/mail/virtual_users
   ```

   Ensure the password is hashed and stored correctly.

2. **Check Authentication Service Configuration:**

   Verify that your email server (e.g., Dovecot) is correctly configured to use the virtual users file:

   **Dovecot Configuration:**

   ```plaintext
   passdb {
     driver = passwd-file
     args = /etc/mail/virtual_users
   }
   ```

   Restart Dovecot to apply changes:

   ```bash
   systemctl restart dovecot
   ```

3. **Verify Permissions on Authentication File:**

   Ensure that the virtual users file has the correct permissions to be read by the mail server:

   ```bash
   ls -l /etc/mail/virtual_users
   ```

   Adjust permissions if necessary:

   ```bash
   chmod 600 /etc/mail/virtual_users
   chown root:root /etc/mail/virtual_users
   ```

## General Troubleshooting Tips

**Check Logs:**

- Always check relevant logs when troubleshooting issues. Logs provide detailed information on what went wrong and can often point you directly to the problem.

**Logs to Check:**

- **System Log:** `/var/log/syslog`
- **Authentication Log:** `/var/log/auth.log`
- **Mail Server Logs:** `/var/log/exim4/mainlog`, `/var/log/dovecot.log`
- **Application Logs:** Check the specific application’s log directory, often under `/var/log/`.

**Common Commands:**

- **`tail -f /var/log/logfile`**: Continuously monitors a log file for new entries.
- **`grep "search_term" /var/log/logfile`**: Searches a log file for a specific term or error message.

**Backup Before Changes:**

- Before making significant changes, such as modifying user files or system configurations, always create a backup. This allows you to revert if something goes wrong.

**Example Backup Command:**

```bash
cp /etc/mail/virtual_users /etc/mail/virtual_users.bak
```

**Use Test Accounts:**

- When implementing new configurations or troubleshooting, use test accounts to avoid disrupting active users. Test accounts can help you experiment with fixes without affecting production services.

**Document Changes:**

- Keep a record of all changes made during troubleshooting. This documentation can help you track what worked, what didn’t, and serve as a reference for future issues.

**Example Documentation:**

```plaintext
Date: 2024-08-27
Issue: Virtual users unable to authenticate
Actions Taken:
  - Verified password hash in /etc/mail/virtual_users
  - Restarted Dovecot service
  - Checked permissions on /etc/mail/virtual_users
Outcome: Issue resolved; users can now authenticate successfully.
```

---
