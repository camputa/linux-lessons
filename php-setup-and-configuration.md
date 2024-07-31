# In-Depth Wiki on PHP, PHP-FPM, and PHP.ini Configuration

Welcome to this comprehensive guide on PHP, PHP-FPM, and PHP.ini configuration for Linux Ubuntu 20.04. This wiki is designed to help you understand these components, their common options, and configurations. Written in a motivational and happy tone, this guide aims to make learning enjoyable and straightforward for those who are new to technology.

## Introduction to PHP

PHP (Hypertext Preprocessor) is a popular server-side scripting language widely used for web development. It is known for its ease of use, flexibility, and ability to embed directly into HTML. PHP powers many dynamic websites and web applications, making it an essential skill for web developers.

## Installing PHP on Ubuntu 20.04

To get started with PHP on Ubuntu 20.04, you'll need to install it using the following commands:

```bash
sudo apt update
sudo apt install php libapache2-mod-php
```

This installs PHP and integrates it with the Apache web server.

## Understanding PHP-FPM

PHP-FPM (FastCGI Process Manager) is an alternative PHP FastCGI implementation with additional features useful for high-load websites. It provides a better way to manage PHP processes, offering advanced process management, better logging, and more efficient handling of high-traffic websites.

### Installing PHP-FPM

To install PHP-FPM, use the following commands:

```bash
sudo apt update
sudo apt install php-fpm
```

### Configuring PHP-FPM

PHP-FPM configurations are primarily located in the `/etc/php/7.4/fpm/` directory (the version may vary). The main configuration file is `php-fpm.conf`, and pool-specific settings are found in `www.conf`.

Key configuration options include:

1. **pm.max_children**: The maximum number of child processes that can be created.
2. **pm.start_servers**: The number of child processes created on startup.
3. **pm.min_spare_servers**: The minimum number of idle child processes.
4. **pm.max_spare_servers**: The maximum number of idle child processes.

Example `www.conf` configuration:

```ini
[www]
user = www-data
group = www-data
listen = /run/php/php7.4-fpm.sock
pm = dynamic
pm.max_children = 10
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3
```

Restart PHP-FPM to apply changes:

```bash
sudo systemctl restart php7.4-fpm
```

## Configuring PHP with PHP.ini

The `php.ini` file is the main configuration file for PHP. It allows you to control various aspects of PHP's behavior, including error reporting, resource limits, and extensions. The `php.ini` file is located in `/etc/php/7.4/apache2/php.ini` for Apache or `/etc/php/7.4/fpm/php.ini` for PHP-FPM.

### Common PHP.ini Configurations

1. **Error Reporting**

   Configure error reporting to display all errors, warnings, and notices during development:

   ```ini
   error_reporting = E_ALL
   display_errors = On
   ```

2. **Memory Limit**

   Set the maximum amount of memory a script is allowed to allocate:

   ```ini
   memory_limit = 128M
   ```

3. **File Uploads**

   Configure the maximum size of an uploaded file:

   ```ini
   upload_max_filesize = 20M
   post_max_size = 25M
   ```

4. **Max Execution Time**

   Set the maximum time a script is allowed to run before being terminated:

   ```ini
   max_execution_time = 30
   ```

5. **Time Zone**

   Set the default time zone used by all date/time functions:

   ```ini
   date.timezone = "America/New_York"
   ```

### Applying PHP.ini Changes

After making changes to the `php.ini` file, restart the web server or PHP-FPM service to apply the new settings:

For Apache:

```bash
sudo systemctl restart apache2
```

For PHP-FPM:

```bash
sudo systemctl restart php7.4-fpm
```

## Secure PHP Configuration

Security is a critical aspect of PHP configuration. Here are some best practices to secure your PHP environment:

1. **Disable Dangerous Functions**

   Disable functions that are not needed and could be exploited:

   ```ini
   disable_functions = exec,passthru,shell_exec,system
   ```

2. **Hide PHP Version**

   Prevent the PHP version from being disclosed in HTTP headers:

   ```ini
   expose_php = Off
   ```

3. **Error Logging**

   Log errors to a file instead of displaying them on the screen:

   ```ini
   log_errors = On
   error_log = /var/log/php_errors.log
   ```

4. **Session Security**

   Secure session handling to prevent session hijacking:

   ```ini
   session.cookie_httponly = On
   session.cookie_secure = On
   ```

## Conclusion

By understanding and properly configuring PHP, PHP-FPM, and PHP.ini, you can optimize your PHP applications for performance, security, and reliability. This guide provides you with the foundational knowledge to get started and encourages you to explore further and experiment with different configurations. Embrace the power of PHP and continue your journey with enthusiasm. Happy coding!