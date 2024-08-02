# Wiki: Displaying Linux Command Output in a PHP File on Ubuntu Server

Welcome to this guide on displaying Linux command output within a PHP file on an Ubuntu server! This wiki will walk you through the process of executing Linux commands from a web form and displaying their results using PHP. Whether you’re looking to build a simple admin tool or just curious about how PHP interacts with the shell, this guide will provide you with a clear and detailed approach.

## Introduction

Running Linux commands from a PHP script allows you to interact with the server's operating system directly. By using a web form to send commands and displaying the output in a PHP file, you can create powerful administrative tools and dynamic web applications. However, be cautious with this capability, as it can pose security risks if not handled properly.

## Prerequisites

Before you start, ensure you have the following:

- **Ubuntu Server**: Ubuntu 20.04 or later.
- **LAMP Stack**: Linux, Apache, MySQL/MariaDB, and PHP installed.
- **Basic Knowledge**: Familiarity with Linux commands and PHP scripting.

## Setting Up the PHP Environment

1. **Install Apache and PHP**

   First, ensure that Apache and PHP are installed on your Ubuntu server. You can install them using the following commands:

   ```bash
   sudo apt update
   sudo apt install apache2 php libapache2-mod-php
   ```

2. **Verify PHP Installation**

   To verify that PHP is correctly installed, create a PHP info file:

   ```bash
   echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
   ```

   Navigate to `http://your-server-ip/info.php` in your web browser to check the PHP information page.

## Creating the PHP Script

1. **Create a PHP File**

   Create a new PHP file in the web root directory (`/var/www/html`). For example, create `command.php`:

   ```bash
   sudo nano /var/www/html/command.php
   ```

2. **Write the PHP Script**

   Here is a basic PHP script to display the output of Linux commands executed via a web form:

   ```php
   <?php
   // Define a function to sanitize and execute commands
   function executeCommand($command) {
       // Sanitize the input to prevent shell injection
       $safeCommand = escapeshellcmd($command);
       // Execute the command and capture the output
       $output = shell_exec($safeCommand);
       return nl2br(htmlspecialchars($output));
   }

   // Check if the form is submitted
   if ($_SERVER["REQUEST_METHOD"] == "POST") {
       $command = $_POST['command'];
       $result = executeCommand($command);
   }
   ?>

   <!DOCTYPE html>
   <html>
   <head>
       <title>Execute Linux Command</title>
   </head>
   <body>
       <h1>Execute Linux Command</h1>
       <form method="post" action="">
           <label for="command">Command:</label>
           <input type="text" id="command" name="command" required>
           <input type="submit" value="Run Command">
       </form>
       <?php
       if (isset($result)) {
           echo "<h2>Output:</h2>";
           echo "<pre>$result</pre>";
       }
       ?>
   </body>
   </html>
   ```

   In this script:
   - The `executeCommand` function sanitizes the command using `escapeshellcmd` to prevent shell injection attacks.
   - `shell_exec` is used to execute the command and capture the output.
   - The output is then displayed safely using `htmlspecialchars` and `nl2br` to handle HTML characters and newlines.

3. **Set Proper Permissions**

   Ensure that the PHP file has the correct permissions for the web server to access it:

   ```bash
   sudo chown www-data:www-data /var/www/html/command.php
   sudo chmod 644 /var/www/html/command.php
   ```

## Security Considerations

Running shell commands from a web interface can be risky. Here are some best practices to enhance security:

1. **Limit Commands**: Restrict the commands that can be executed. You might consider using a whitelist of allowed commands instead of allowing any command.

2. **Use HTTPS**: Ensure your server uses HTTPS to encrypt data transmitted between the user and the server.

3. **Authentication and Authorization**: Restrict access to the command execution page by requiring user authentication.

4. **Avoid Shell Injection**: Always sanitize user input using `escapeshellcmd` and `htmlspecialchars`.

5. **Log Usage**: Consider logging command usage for monitoring and auditing purposes.

## Testing the Setup

1. **Access the Web Form**

   Open your web browser and navigate to `http://your-server-ip/command.php`.

2. **Run a Command**

   Enter a simple command, such as `ls` or `date`, and click "Run Command" to see the output.

3. **Verify Output**

   Check that the output is displayed correctly on the web page. Ensure there are no errors and that the command executes as expected.

## Conclusion

Congratulations! You’ve set up a PHP script on your Ubuntu server to execute Linux commands and display their output. This capability can be incredibly useful for administrative tasks and automation. However, always be cautious about the security implications and take measures to protect your server.

Embrace the power of PHP and Linux command execution with confidence, and enjoy the possibilities that come with this powerful combination. Happy coding and secure server management!