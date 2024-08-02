# Step-by-Step Guide: Daily SSH Access Report on Ubuntu 22.04

This guide provides step-by-step instructions to set up a daily cron job that generates a formatted text report of Linux users who attempted, failed, or successfully gained access to your Ubuntu 22.04 machine via SSH. The report will include the username, IP address, and timestamp of each attempt.

## Step 1: Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```
- **Explanation**: Ensures that all system packages are up-to-date.

## Step 2: Install Required Packages

```bash
sudo apt install mailutils
```
- **Explanation**: Installs the `mailutils` package, which is required for sending emails via the command line.

## Step 3: Create the SSH Access Report Script

Create a script that will parse the log files and generate the report.

```bash
sudo nano /usr/local/bin/ssh_access_report.sh
```

Add the following content to the script:

```bash
#!/bin/bash

# Define the output file
OUTPUT_FILE="/var/log/ssh_access_report.txt"

# Generate the report header
echo "SSH Access Report - $(date)" > $OUTPUT_FILE
echo "===================================" >> $OUTPUT_FILE

# Get successful SSH logins
echo "Successful SSH Logins:" >> $OUTPUT_FILE
grep "Accepted" /var/log/auth.log | awk '{print "User: " $9 ", IP: " $11 ", Timestamp: " $1 " " $2 " " $3}' >> $OUTPUT_FILE
echo "" >> $OUTPUT_FILE

# Get failed SSH login attempts
echo "Failed SSH Login Attempts:" >> $OUTPUT_FILE
grep "Failed password" /var/log/auth.log | awk '{print "User: " $9 ", IP: " $11 ", Timestamp: " $1 " " $2 " " $3}' >> $OUTPUT_FILE
echo "" >> $OUTPUT_FILE

# Get invalid user login attempts
echo "Invalid User Login Attempts:" >> $OUTPUT_FILE
grep "Invalid user" /var/log/auth.log | awk '{print "User: " $8 ", IP: " $10 ", Timestamp: " $1 " " $2 " " $3}' >> $OUTPUT_FILE
echo "" >> $OUTPUT_FILE

# Send the report via email
mail -s "Daily SSH Access Report" youremail@example.com < $OUTPUT_FILE
```

- **Explanation**: This script parses the `/var/log/auth.log` file to extract information about successful SSH logins, failed SSH login attempts, and invalid user login attempts. It formats this information into a report and sends it via email.

## Step 4: Make the Script Executable

```bash
sudo chmod +x /usr/local/bin/ssh_access_report.sh
```
- **Explanation**: Makes the script executable.

## Step 5: Set Up a Daily Cron Job

Create a cron job to run the script daily.

```bash
sudo crontab -e
```

Add the following line to the crontab file:

```plaintext
0 0 * * * /usr/local/bin/ssh_access_report.sh
```

- **Explanation**: This cron job runs the `ssh_access_report.sh` script every day at midnight.

## Step 6: Verify Email Configuration

Ensure that your system is configured to send emails. Test it by sending a test email:

```bash
echo "Test email" | mail -s "Test" youremail@example.com
```

- **Explanation**: Sends a test email to verify that the email configuration is working correctly.

## Conclusion

By following these steps, you have set up a daily cron job on your Ubuntu 22.04 machine that generates a formatted text report of SSH access attempts. The report includes usernames, IP addresses, and timestamps, and is sent to your email address daily. This setup helps in monitoring and securing your system by keeping track of all login attempts.