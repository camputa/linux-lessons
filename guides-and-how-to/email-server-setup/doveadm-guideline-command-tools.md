# Starting Guide for `doveadm` Command Line Usage on Ubuntu 22.04

The `doveadm` command is a powerful tool for managing and troubleshooting Dovecot, the popular IMAP and POP3 server. This guide provides a starting point for using `doveadm` on Ubuntu 22.04, covering common options, troubleshooting steps, and best practices.

## 1. **Introduction to `doveadm`**

`doveadm` is the command-line utility provided by Dovecot for performing a variety of administrative tasks. It can be used for managing mailboxes, performing maintenance, monitoring server status, and debugging issues.

## 2. **Common `doveadm` Commands**

Here are some essential `doveadm` commands that you’ll use frequently:

### 2.1 **Mailbox Management**

- **List Mailboxes**: Display a list of mailboxes for a specific user.
  ```bash
  doveadm mailbox list -u user@example.com
  ```

- **Search Emails**: Search for emails matching specific criteria.
  ```bash
  doveadm search -u user@example.com mailbox INBOX SUBJECT "important"
  ```

- **Expunge Deleted Emails**: Permanently delete emails marked for deletion in a specific mailbox.
  ```bash
  doveadm expunge -u user@example.com mailbox INBOX DELETED
  ```

- **Copy Emails**: Copy emails from one mailbox to another.
  ```bash
  doveadm copy -u user@example.com INBOX Trash SUBJECT "important"
  ```

### 2.2 **User Management**

- **Authenticate a User**: Test the authentication for a user.
  ```bash
  doveadm auth test user@example.com
  ```

- **Sync Mailbox**: Synchronize a user’s mailbox with the server.
  ```bash
  doveadm sync -u user@example.com
  ```

- **Quota Management**: Check a user’s mailbox quota.
  ```bash
  doveadm quota get -u user@example.com
  ```

### 2.3 **Server Monitoring**

- **Log Errors**: Check for errors in Dovecot’s logs.
  ```bash
  doveadm log errors
  ```

- **Server Status**: Monitor the status of the Dovecot server.
  ```bash
  doveadm stats dump
  ```

- **Connections**: List all active connections to the Dovecot server.
  ```bash
  doveadm who
  ```

## 3. **Troubleshooting with `doveadm`**

`doveadm` is particularly useful for troubleshooting common issues in Dovecot. Here’s how to address some typical problems:

### 3.1 **Problem: User Cannot Authenticate**

- **Solution**: Use the `doveadm auth test` command to test the user’s authentication:
  ```bash
  doveadm auth test user@example.com
  ```
  This command will output detailed information about the authentication process, including whether the credentials are correct and if there are any configuration issues.

### 3.2 **Problem: Mailbox Not Syncing**

- **Solution**: Force a synchronization of the user’s mailbox with:
  ```bash
  doveadm sync -u user@example.com
  ```
  If the sync fails, check the Dovecot logs for errors using:
  ```bash
  doveadm log errors
  ```

### 3.3 **Problem: Disk Space Running Low**

- **Solution**: Identify large mailboxes using:
  ```bash
  doveadm quota recalc -A
  ```
  Then, expunge unnecessary or deleted emails:
  ```bash
  doveadm expunge -A mailbox INBOX SENTBEFORE 30d
  ```

### 3.4 **Problem: Performance Issues**

- **Solution**: Monitor server performance and identify bottlenecks with:
  ```bash
  doveadm stats dump
  ```
  Check the number of active connections using:
  ```bash
  doveadm who
  ```

## 4. **Best Practices for Using `doveadm`**

To make the most out of `doveadm`, follow these best practices:

### 4.1 **Regular Monitoring**

- Regularly use `doveadm` to monitor your Dovecot server’s status and performance. Commands like `doveadm stats dump` and `doveadm log errors` can help you catch issues early before they impact users.

### 4.2 **Automate Routine Tasks**

- Automate common maintenance tasks such as expunging old emails or syncing mailboxes with cron jobs. This ensures your server remains efficient and reduces manual workload.

### 4.3 **Use Verbose and Debugging Options**

- When troubleshooting, use the `-v` (verbose) or `-D` (debug) options to get more detailed output. For example:
  ```bash
  doveadm -v auth test user@example.com
  ```
  This can provide more context to help identify issues.

### 4.4 **Secure Access to `doveadm`**

- Restrict access to `doveadm` by limiting its usage to administrative users only. Since `doveadm` can perform critical actions, it should not be accessible to unauthorized users.

### 4.5 **Keep Documentation Handy**

- Always refer to the official Dovecot documentation or the `doveadm` man page (`man doveadm`) for detailed explanations of commands and options.

## Conclusion

`doveadm` is an indispensable tool for managing and troubleshooting Dovecot on Ubuntu 22.04. By mastering the common commands, understanding how to troubleshoot typical issues, and following best practices, you can ensure your Dovecot server remains secure, efficient, and reliable. Regular use of `doveadm` will make it easier to maintain and monitor your email server, keeping it in top shape for your users.