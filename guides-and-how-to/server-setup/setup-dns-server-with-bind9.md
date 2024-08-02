# Comprehensive Guide to Setting Up a DNS Server with BIND9 on Ubuntu 20.04

Welcome to your journey into the world of DNS with BIND9 on Ubuntu 20.04! Setting up a Domain Name System (DNS) server can be an empowering experience, providing you with greater control over how domain names are resolved and managed. This guide is designed to help you through each step of setting up and configuring BIND9, ensuring you understand the process and feel confident in your DNS management skills.

## What is BIND9?

BIND9 (Berkeley Internet Name Domain version 9) is one of the most widely used DNS server software. It translates domain names (like `example.com`) into IP addresses that computers use to identify each other on the network. Think of BIND9 as the phone book for the internet, converting human-friendly names into the numerical addresses that machines understand.

## Installing BIND9

First things first, let’s get BIND9 installed on your Ubuntu 20.04 system. Start by updating your package list and upgrading your system to ensure everything is up-to-date:

```bash
sudo apt update
sudo apt upgrade -y
```

With your system updated, you can now install BIND9 and its associated utilities:

```bash
sudo apt install bind9 bind9utils bind9-doc dnsutils
```

The `bind9` package contains the DNS server software, `bind9utils` includes useful command-line tools, `bind9-doc` provides documentation, and `dnsutils` offers additional DNS utilities for testing and troubleshooting.

## Configuring BIND9

Once installed, it’s time to configure BIND9. The main configuration file for BIND9 is located at `/etc/bind/named.conf`. This file includes other configuration files and sets up the basic parameters for your DNS server.

### Setting Up Zones

Zones are fundamental in DNS, representing different domains and their respective records. To manage zones, you need to define them in the configuration files. The primary files involved are `/etc/bind/named.conf.local`, `/etc/bind/named.conf.default-zones`, and your zone files.

#### 1. Edit Zone Configuration

Open the zone configuration file for editing:

```bash
sudo nano /etc/bind/named.conf.local
```

Add your zone definitions. For example, if you’re setting up a domain `example.com`, your configuration might look like this:

```plaintext
zone "example.com" {
    type master;
    file "/etc/bind/db.example.com";
};

zone "1.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/db.192.168.1";
};
```

This configuration tells BIND9 that `example.com` and its reverse lookup (mapping IP addresses back to domain names) will be managed by files located in `/etc/bind`.

#### 2. Create Zone Files

Now, create the zone file for `example.com`:

```bash
sudo nano /etc/bind/db.example.com
```

Add the following sample configuration to the file:

```plaintext
$TTL    86400
@       IN      SOA     ns1.example.com. admin.example.com. (
                          2024072901 ; Serial
                          3600       ; Refresh
                          1800       ; Retry
                          1209600    ; Expire
                          86400 )    ; Minimum TTL
;
@       IN      NS      ns1.example.com.
@       IN      A       192.168.1.1
ns1     IN      A       192.168.1.1
www     IN      A       192.168.1.2
mail    IN      A       192.168.1.3
@       IN      MX      10 mail.example.com.
```

This file defines several records:
- **SOA Record**: Marks the start of authority for the domain.
- **NS Record**: Specifies the nameserver for the domain.
- **A Record**: Maps domain names to IP addresses.
- **MX Record**: Specifies the mail server for the domain.

For the reverse zone file, `/etc/bind/db.192.168.1`, which maps IP addresses back to domain names, you would use a similar format:

```plaintext
$TTL    86400
@       IN      SOA     ns1.example.com. admin.example.com. (
                          2024072901 ; Serial
                          3600       ; Refresh
                          1800       ; Retry
                          1209600    ; Expire
                          86400 )    ; Minimum TTL
;
@       IN      NS      ns1.example.com.
1       IN      PTR     example.com.
2       IN      PTR     www.example.com.
3       IN      PTR     mail.example.com.
```

### Verifying Configuration

Before restarting BIND9, it’s crucial to verify your configuration files to ensure there are no syntax errors. Use the following command:

```bash
sudo named-checkconf
sudo named-checkzone example.com /etc/bind/db.example.com
sudo named-checkzone 1.168.192.in-addr.arpa /etc/bind/db.192.168.1
```

These commands check the syntax of your configuration files and zone files, helping to catch any mistakes before they cause issues.

### Restarting BIND9

With the configuration files in place and verified, restart the BIND9 service to apply the changes:

```bash
sudo systemctl restart bind9
```

Enable BIND9 to start on boot:

```bash
sudo systemctl enable bind9
```

## Testing Your DNS Server

Once BIND9 is up and running, it’s time to test your setup. Use `dig` or `nslookup` to query your DNS server:

```bash
dig @localhost example.com
dig @localhost www.example.com
dig @localhost -x 192.168.1.2
```

These commands query your DNS server for domain name resolutions and reverse lookups, verifying that your configurations are working correctly.

## Common Options and Configurations

BIND9 offers a range of options to customize its behavior. Here are a few commonly used configurations:

- **`allow-query`**: Controls which IP addresses are allowed to query your DNS server. For example, `allow-query { 192.168.1.0/24; };` allows queries from the local network.

- **`allow-transfer`**: Specifies which IP addresses are allowed to transfer zone data. Useful for setting up secondary (slave) DNS servers.

- **`recursion`**: Determines whether your DNS server will perform recursive queries. Setting `recursion no;` turns off recursion, making the server authoritative only for the zones it serves.

## Security Best Practices

To keep your DNS server secure, consider these best practices:

1. **Limit Access**: Restrict query and transfer access to trusted IP addresses to prevent unauthorized use of your server.

2. **Regular Updates**: Keep BIND9 and your system updated to protect against known vulnerabilities.

3. **Monitor Logs**: Regularly check DNS logs for unusual activity. Logs can be found in `/var/log/syslog` or `/var/log/bind`.

4. **Implement DNSSEC**: Consider configuring DNSSEC (DNS Security Extensions) to add an additional layer of security to your DNS records.

## Conclusion

Setting up a DNS server with BIND9 on Ubuntu 20.04 is an empowering step toward mastering network management. By understanding and implementing DNS configurations, you’re gaining valuable skills that enhance your ability to manage and secure networks. Remember, every configuration you make brings you closer to becoming a DNS expert. Keep experimenting, learning, and exploring—your journey in the world of DNS is just beginning. Happy DNS management!