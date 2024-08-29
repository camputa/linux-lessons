# Automation and Scripting

In a multi-domain hosting environment, managing virtual users manually can quickly become cumbersome, especially as the number of domains and users increases. Automation through scripting allows you to streamline the process, reducing errors and ensuring consistency across your system. This section covers how to automate the creation of virtual email-only users for multiple domains, using a custom script to handle the setup efficiently.

## Why Automate?

Automation is crucial in system administration for several reasons:

- **Consistency:** Scripts ensure that the same process is followed every time, reducing the chance of human error.
- **Efficiency:** Automating repetitive tasks saves time, especially when managing a large number of users or domains.
- **Scalability:** As your hosting environment grows, automation helps you scale your operations without a proportional increase in administrative overhead.
- **Maintainability:** Automated scripts are easier to maintain and update than manual procedures, especially when dealing with complex setups.

## Creating a Script to Automate Virtual User Setup

Below is a Bash script that automates the creation of virtual email-only users for multiple domains. This script will:

1. **Accept User Input:** Collect details about the user, domain, and password.
2. **Encrypt the Password:** Use Dovecot’s password utility to encrypt the password securely.
3. **Create Mail Directories:** Ensure the mail directory structure exists for each user.
4. **Update the Virtual User File:** Add the new user’s credentials and mail directory to the `virtual_users` file.

---

**Script: `create_virtual_user.sh`**

```bash
#!/bin/bash

# Function to create a virtual email user
create_virtual_user() {
  local email=$1
  local domain=$2
  local password=$3
  local mail_dir="/var/mail/virtual/$domain/$email/"

  # Encrypt the password using Dovecot's utility
  local encrypted_password=$(doveadm pw -s SHA512-CRYPT -p "$password")

  # Create the mail directory if it doesn't exist
  if [ ! -d "$mail_dir" ]; then
    mkdir -p "$mail_dir"
    chown -R vmail:vmail "$mail_dir"
    chmod -R 700 "$mail_dir"
  fi

  # Add the user to the virtual_users file
  echo "$email@$domain:$encrypted_password:maildir:$mail_dir" >> /etc/mail/virtual_users

  echo "Virtual user $email@$domain created successfully."
}

# Check if sufficient arguments are provided
if [ "$#" -ne 3 ]; then
  echo "Usage: $0 <email> <domain> <password>"
  exit 1
fi

# Execute the function with provided arguments
create_virtual_user "$1" "$2" "$3"
```

---

## Detailed Breakdown of the Script

**1. Script Header**

```bash
#!/bin/bash
```

- **`#!/bin/bash`**: This line indicates that the script should be run using the Bash shell.

**2. Function Definition: `create_virtual_user()`**

```bash
create_virtual_user() {
  local email=$1
  local domain=$2
  local password=$3
  local mail_dir="/var/mail/virtual/$domain/$email/"
```

- **`create_virtual_user()`**: Defines a function that takes three arguments: the email address, domain, and password.
- **`local email=$1`, `local domain=$2`, `local password=$3`**: These lines assign the script arguments to local variables for easier reference.
- **`local mail_dir="/var/mail/virtual/$domain/$email/"`**: Sets the path where the user’s mail will be stored, based on the domain and email address.

**3. Encrypting the Password**

```bash
local encrypted_password=$(doveadm pw -s SHA512-CRYPT -p "$password")
```

- **`doveadm pw -s SHA512-CRYPT -p "$password"`**: Uses Dovecot’s `doveadm` tool to encrypt the user’s password using the `SHA512-CRYPT` method, which is secure and widely supported.
- **`local encrypted_password`**: Stores the encrypted password in a variable for later use.

**4. Creating the Mail Directory**

```bash
if [ ! -d "$mail_dir" ]; then
  mkdir -p "$mail_dir"
  chown -R vmail:vmail "$mail_dir"
  chmod -R 700 "$mail_dir"
fi
```

- **`if [ ! -d "$mail_dir" ]; then`**: Checks if the mail directory already exists. If it doesn’t, the script proceeds to create it.
- **`mkdir -p "$mail_dir"`**: Creates the mail directory, including any necessary parent directories.
- **`chown -R vmail:vmail "$mail_dir"`**: Sets the ownership of the directory and its contents to the `vmail` user and group, which is typically used by Dovecot.
- **`chmod -R 700 "$mail_dir"`**: Sets permissions to ensure that only the `vmail` user can access the directory, enhancing security.

**5. Updating the Virtual Users File**

```bash
echo "$email@$domain:$encrypted_password:maildir:$mail_dir" >> /etc/mail/virtual_users
```

- **`echo "$email@$domain:$encrypted_password:maildir:$mail_dir"`**: Formats the virtual user’s details for the flat file.
- **`>> /etc/mail/virtual_users`**: Appends the new user’s information to the `virtual_users` file, ensuring that it’s added to the existing list of users.

**6. Final Output**

```bash
echo "Virtual user $email@$domain created successfully."
```

- **`echo`**: Provides feedback to the administrator that the user has been created successfully.

**7. Argument Check**

```bash
if [ "$#" -ne 3 ]; then
  echo "Usage: $0 <email> <domain> <password>"
  exit 1
fi
```

- **`if [ "$#" -ne 3 ]`**: Checks if the correct number of arguments is provided. If not, it displays a usage message and exits the script.
- **`exit 1`**: Exits the script with an error code if the arguments are insufficient.

**8. Executing the Function**

```bash
create_virtual_user "$1" "$2" "$3"
```

- **`create_virtual_user "$1" "$2" "$3"`**: Calls the function with the provided arguments (email, domain, and password).

---

### Using the Script

To use this script:

1. **Save the script** as `create_virtual_user.sh`.
2. **Make it executable**:

   ```bash
   chmod +x create_virtual_user.sh
   ```

3. **Run the script** with the necessary arguments:

   ```bash
   ./create_virtual_user.sh user1 domain.com password123
   ```

   Replace `user1`, `domain.com`, and `password123` with the actual email username, domain, and desired password.

---
