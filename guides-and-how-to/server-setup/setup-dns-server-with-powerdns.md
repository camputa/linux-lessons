# **PowerDNS Configuration and Administration Guide (SQLite Backend)**

This wiki provides a comprehensive guide for setting up, configuring, and administering DNS services using PowerDNS with an SQLite backend on Ubuntu 20.04. The guide covers installation, DNS zone management, security best practices, automation, and troubleshooting. It’s designed to help both beginners and experienced administrators maintain a secure and efficient DNS infrastructure.

---

## **Introduction to PowerDNS**

PowerDNS is a powerful, open-source DNS server known for its flexibility and scalability. It supports multiple backends, including SQLite, which is a lightweight database option suitable for small to medium-sized DNS setups. Using SQLite with PowerDNS provides an easy-to-manage and portable solution for DNS management.

---

## **Installation and Initial Setup**

**Installing PowerDNS with SQLite on Ubuntu 20.04:**

To install PowerDNS with the SQLite backend, follow these steps:

**Step-by-Step Installation:**

1. **Update Package List:**

   Ensure your system packages are up-to-date:

   ```bash
   sudo apt update
   ```

2. **Install PowerDNS and SQLite:**

   Install PowerDNS along with the SQLite backend:

   ```bash
   sudo apt install pdns-server pdns-backend-sqlite3 sqlite3 -y

   sudo systemctl stop systemd-resolved
   #sudo systemctl disable --now systemd-resolved
   #sudo rm -rf /etc/resolv.conf
   #echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
   ```

3. **Configure PowerDNS to Use SQLite Backend:**

   Create the SQLite database and configure PowerDNS to use it:

   ```bash
   sudo mkdir -p /var/lib/powerdns
   sudo sqlite3 /var/lib/powerdns/pdns.sqlite3 < /usr/share/doc/pdns-backend-sqlite3/schema.sqlite3.sql
   sudo chown -R pdns:pdns /var/lib/powerdns
   ```

   Edit the PowerDNS configuration file `/etc/powerdns/pdns.conf`:

   ```bash
   sudo vim /etc/powerdns/pdns.conf
   ```

   Add the following configuration:

   ```plaintext
   launch=gsqlite3
   gsqlite3-database=/var/lib/powerdns/pdns.sqlite3
   ```

4. **Confirm the SQLite Database Schema:**

   Import the PowerDNS schema into the SQLite database:

   ```bash
   sudo -u pdns sqlite3 /var/lib/powerdns/pdns.sqlite3
   .databases
   .tables
   .exit
   ```

5. **Restart PowerDNS:**

   Restart the PowerDNS service to apply the changes:

   ```bash
   sudo systemctl restart pdns
   ```

   Enable PowerDNS to start on boot:

   ```bash
   sudo systemctl enable pdns
   ```

---

## **Configuring DNS Zones and Records Using `pdnsutil`**

This section provides a detailed guide on configuring DNS zones and records using the `pdnsutil` command-line tool. `pdnsutil` simplifies managing DNS zones and records with PowerDNS, allowing you to create, update, and configure various types of DNS records such as A, CNAME, MX, TXT, and NS.

---

### **1. Creating a DNS Zone**

Before adding records, you must create a DNS zone. A DNS zone is a collection of DNS records for a particular domain.

**Creating a New Zone with `pdnsutil create-zone`:**

The `create-zone` option allows you to create a new DNS zone for a domain.

**Example Command:**

```bash
sudo -u pdns pdnsutil create-zone example.com ns1.example.com
```

**Breakdown:**

- **`example.com`**: The domain for which the zone is being created.
- **`ns1.example.com`**: The name server for the domain. This should be a fully qualified domain name (FQDN).

---

### **2. Adding DNS Records**

Once the zone is created, you can add various DNS records. Each type of DNS record serves a different purpose.

**2.1 Adding an A Record**

An A record maps a domain name to an IPv4 address.

**Example Command:**

```bash
sudo -u pdns pdnsutil add-record example.com www A 192.168.1.100
```

**Breakdown:**

- **`www`**: The subdomain to which the A record applies.
- **`A`**: Specifies that this is an A record.
- **`192.168.1.100`**: The IPv4 address to which the subdomain will point.

**2.2 Adding a CNAME Record**

A CNAME record creates an alias for another domain name.

**Example Command:**

```bash
sudo -u pdns pdnsutil add-record example.com mail CNAME mailserver.example.com
```

**Breakdown:**

- **`mail`**: The alias for the domain.
- **`CNAME`**: Specifies that this is a CNAME record.
- **`mailserver.example.com`**: The canonical name to which the alias points.

**2.3 Adding an MX Record**

An MX record specifies the mail servers responsible for receiving emails for the domain.

**Example Command:**

```bash
sudo -u pdns pdnsutil add-record example.com '' MX '10 mail.example.com'
```

**Breakdown:**

- **`@`**: The root domain (example.com).
- **`MX`**: Specifies that this is an MX record.
- **`10`**: The priority of the mail server (lower values indicate higher priority).
- **`mail.example.com`**: The FQDN of the mail server.

**2.4 Adding a TXT Record**

A TXT record is used to store text-based data, often for verification purposes.

**Example Command:**

```bash
sudo -u pdns pdnsutil add-record example.com @ TXT "v=spf1 mx -all"
```

**Breakdown:**

- **`@`**: The root domain (example.com).
- **`TXT`**: Specifies that this is a TXT record.
- **`"v=spf1 mx -all"`**: The content of the TXT record, often used for SPF records in email security.

**2.5 Adding an NS Record**

An NS record specifies the authoritative DNS servers for the domain.

**Example Command:**

```bash
sudo -u pdns pdnsutil add-record example.com @ NS ns1.example.com
```

**Breakdown:**

- **`@`**: The root domain (example.com).
- **`NS`**: Specifies that this is an NS record.
- **`ns1.example.com`**: The FQDN of the authoritative DNS server.

---

### **3. Updating and Modifying DNS Records**

You can update or modify existing DNS records using the `pdnsutil` command.

**3.1 Updating a Record**

To update an existing record, use the `replace-rrset` option:

**Example Command:**

```bash
sudo -u pdns pdnsutil replace-rrset example.com www A 192.168.1.101
```

**Breakdown:**

- **`replace-rrset`**: Replaces the existing resource record set (RRset) for the specified domain and type.
- **`192.168.1.101`**: The new IPv4 address for the A record.

**3.2 Deleting a Record**

To delete a DNS record, use the `delete-record` option:

**Example Command:**

```bash
sudo -u pdns pdnsutil delete-record example.com www A
```

**Breakdown:**

- **`delete-record`**: Removes the specified DNS record from the zone.
- **`www`**: The subdomain of the record to delete.
- **`A`**: Specifies the type of the record to delete.

---

### **4. Verifying and Committing Changes**

After making changes, it’s important to verify and commit them.

**4.1 Verifying the Zone:**

To check the syntax and consistency of the DNS zone, use the `check-zone` option:

**Example Command:**

```bash
sudo -u pdns pdnsutil check-zone example.com
```

This command will validate the zone and highlight any issues.

**4.2 Rectifying the Zone:**

To ensure all DNSSEC-related information is correct and up-to-date, use the `rectify-zone` option:

**Example Command:**

```bash
sudo -u pdns pdnsutil rectify-zone example.com
```

**4.3 Committing Changes:**

If you’ve made changes using the API or backend, commit them to the zone database:

**Example Command:**

```bash
sudo -u pdns pdnsutil commit-zone example.com
```

---

## **Configuring DNS Zones and Records**

**Common DNS Records:**

- **A Record**: Maps a domain name to an IPv4 address.
- **AAAA Record**: Maps a domain name to an IPv6 address.
- **CNAME Record**: An alias for another domain name.
- **MX Record**: Specifies mail servers for the domain.
- **TXT Record**: Used for various text-based data, often for verification purposes.
- **NS Record**: Specifies authoritative DNS servers for the domain.

---

## **Discussion on SOA Records in PowerDNS**

The Start of Authority (SOA) record is a critical component in DNS management, as it defines the authoritative information about a DNS zone. This includes details like the primary name server, the responsible party's email address, and essential timing information for the zone's refresh and retry intervals. Proper administration of SOA records is vital, especially in a multi-domain DNS server setup where accurate and consistent DNS data is crucial.

---

### **1. Understanding SOA Records**

An SOA record contains several key fields:

- **Primary Name Server**: The authoritative DNS server for the zone.
- **Hostmaster Email**: The email address of the person responsible for the zone (formatted with a dot instead of @).
- **Serial Number**: A version number that changes with each update to the zone, crucial for synchronizing changes across DNS servers.
- **Refresh Interval**: How often secondary servers should check for updates from the primary server.
- **Retry Interval**: The interval secondary servers wait before retrying a failed refresh.
- **Expire Interval**: The time after which the zone data is considered invalid if not updated.
- **Minimum TTL**: The default time-to-live for all records in the zone.

**Example SOA Record:**

```text
example.com. IN SOA ns1.example.com. hostmaster.example.com. (
    2024082701 ; Serial
    3600       ; Refresh
    900        ; Retry
    1209600    ; Expire
    3600       ; Minimum TTL
)
```

---

### **2. Common Challenges with SOA Records**

Managing SOA records can be complex, particularly in environments with multiple domains and servers. Some common challenges include:

**2.1 Synchronization Issues**

- **Problem**: The serial number is not updated correctly, leading to synchronization issues between primary and secondary servers.
- **Solution**: Always increment the serial number after making changes to the zone. The most common format is `YYYYMMDDnn`, where `nn` is the revision number for the day.

**2.2 Incorrect Timing Settings**

- **Problem**: Improper configuration of the refresh, retry, and expire intervals can lead to excessive or insufficient updates, potentially causing downtime or outdated DNS records.
- **Solution**: Use standard timings unless your specific setup requires customization. For example:
  - **Refresh**: 3600 seconds (1 hour)
  - **Retry**: 900 seconds (15 minutes)
  - **Expire**: 1209600 seconds (14 days)
  - **Minimum TTL**: 3600 seconds (1 hour)

**2.3 Misconfigured Primary Name Server**

- **Problem**: The primary name server in the SOA record does not match the actual authoritative server, leading to DNS resolution issues.
- **Solution**: Ensure that the primary name server field in the SOA record correctly reflects the designated authoritative DNS server for the zone.

---

### **3. Best Practices for Administering SOA Records in a Multi-Domain DNS Server**

Managing SOA records across multiple domains on a single DNS server requires careful planning and consistency. Here are some best practices:

**3.1 Consistent Serial Number Management**

In a multi-domain environment, it’s crucial to maintain a consistent approach to serial numbers. Automate the process where possible, using scripts to increment serial numbers whenever a zone file is updated.

**3.2 Automating SOA Record Management**

To reduce the risk of human error, automate the creation and updating of SOA records. This can be done using configuration management tools like Ansible, or through custom scripts that ensure all fields are correctly populated and consistent across domains.

**3.3 Regular Audits**

Periodically audit SOA records across all domains to ensure consistency and correctness. Use tools like `pdnsutil` to verify zone integrity and `check-zone` commands to validate SOA records.

**Example Audit Script**:

```bash
#!/bin/bash
domains=("example.com" "another-domain.com" "third-domain.com")

for domain in "${domains[@]}"; do
    echo "Checking SOA record for $domain"
    pdnsutil check-zone $domain
done
```

**3.4 Adjusting Timing Values Based on Traffic**

For high-traffic domains, consider lowering the refresh and retry intervals to ensure faster propagation of changes. Conversely, for low-traffic or stable zones, these intervals can be increased to reduce unnecessary traffic.

---

### **4. Troubleshooting SOA Record Issues**

**4.1 Serial Number Not Updating**

If the serial number isn’t updating, verify that the zone file is being correctly updated and that the serial number format is correct. If using automated tools, ensure they are configured to increment the serial number appropriately.

**4.2 Propagation Delays**

If changes to the DNS zone are not propagating as expected, check the refresh and retry intervals in the SOA record. Lowering these values temporarily can help speed up propagation.

**4.3 Incorrect Primary Name Server**

If DNS queries are failing, ensure that the primary name server in the SOA record matches the actual authoritative server. Use the `pdnsutil` tool to rectify any discrepancies.

---

## **Adding or Updating an SOA Record in PowerDNS**

This section will guide you through the process of adding or updating an SOA record for a domain in PowerDNS. Managing SOA records effectively is crucial for the smooth operation of DNS services, particularly in environments hosting multiple domains.

---

### **1. Adding an SOA Record**

When you create a new DNS zone using PowerDNS, an SOA record is typically generated automatically. However, there may be cases where you need to manually add an SOA record.

**1.1 Using `pdnsutil` to Add an SOA Record**

To add an SOA record manually, use the `pdnsutil` command.

**Example Command:**

```bash
sudo pdnsutil add-record example.com @ SOA ns1.example.com hostmaster.example.com 2024082701 3600 900 1209600 3600
```

**Breakdown:**

- **`example.com`**: The domain for which the SOA record is being added.
- **`@`**: Specifies that the record applies to the root domain.
- **`SOA`**: The type of DNS record being added.
- **`ns1.example.com`**: The primary name server.
- **`hostmaster.example.com`**: The email address of the domain administrator (formatted with a dot instead of `@`).
- **`2024082701`**: The serial number in the `YYYYMMDDnn` format.
- **`3600`**: The refresh interval in seconds (1 hour).
- **`900`**: The retry interval in seconds (15 minutes).
- **`1209600`**: The expire interval in seconds (14 days).
- **`3600`**: The minimum TTL in seconds (1 hour).

---

### **2. Updating an Existing SOA Record**

If you need to update an existing SOA record, you can also use the `pdnsutil` command to make the necessary changes.

**2.1 Using `pdnsutil` to Update an SOA Record**

To update the SOA record, use the `replace-rrset` option in `pdnsutil`.

**Example Command:**

```bash
sudo pdnsutil replace-rrset example.com @ SOA ns1.example.com hostmaster.example.com 2024082702 3600 900 1209600 3600
```

**Breakdown:**

- **`replace-rrset`**: Replaces the existing resource record set (RRset) for the domain.
- **`2024082702`**: Updated serial number, incremented to ensure proper synchronization.
- The remaining fields should be updated as necessary to reflect the current configuration requirements.

---

### **3. Verifying the SOA Record**

After adding or updating the SOA record, it’s important to verify that the changes have been applied correctly.

**3.1 Using `pdnsutil` to Check the Zone**

To verify the SOA record, you can check the zone using the `check-zone` command:

**Example Command:**

```bash
sudo pdnsutil check-zone example.com
```

This command will validate the zone and confirm that the SOA record is correctly configured.

**3.2 Using `dig` to Query the SOA Record**

You can also use the `dig` command to query the SOA record directly from the DNS server:

**Example Command:**

```bash
dig +short SOA example.com
```

This will return the current SOA record for the domain, allowing you to verify the primary name server, email address, serial number, and other fields.

---

### **4. Common Issues and Solutions**

**4.1 Serial Number Not Incrementing**

- **Problem**: If the serial number is not incrementing, changes to the DNS zone may not propagate correctly.
- **Solution**: Ensure that you manually increment the serial number each time you update the SOA record, following the `YYYYMMDDnn` format.

**4.2 Incorrect Primary Name Server or Email Address**

- **Problem**: Incorrect information in the SOA record can lead to DNS resolution issues or failed email notifications.
- **Solution**: Double-check the primary name server and email address fields when adding or updating the SOA record to ensure they are correct.

**4.3 Propagation Delays**

- **Problem**: Changes to the SOA record may not propagate as quickly as expected.
- **Solution**: Verify the refresh and retry intervals to ensure they are appropriate for your DNS infrastructure. Lowering these values temporarily can speed up propagation.

---

## **DNS Security Best Practices**

**Restrict Zone Transfers:**

Zone transfers allow DNS records to be copied from one server to another. Restrict zone transfers to trusted IP addresses to prevent unauthorized access.

**Configuring Zone Transfers:**

Edit the PowerDNS configuration to allow transfers only from specific IP addresses:

```plaintext
allow-axfr-ips=192.168.1.2
```

**Implement DNSSEC:**

DNSSEC (DNS Security Extensions) provides a layer of security by signing DNS data. This ensures that the information received from a DNS server is authentic.

**Enabling DNSSEC:**

1. **Edit PowerDNS Configuration:**

   Enable DNSSEC by adding the following line to `/etc/powerdns/pdns.conf`:

   ```plaintext
   dnssec=on
   ```

2. **Sign the Zone:**

   Use the PowerDNS utility to sign the zone:

   ```bash
   sudo -u pdns pdnsutil secure-zone example.com
   sudo -u pdns pdnsutil rectify-zone example.com
   ```

3. **Add the DS Record to the Parent Zone:**

   Export the DS record and submit it to your domain registrar:

   ```bash
   sudo -u pdns pdnsutil show-zone example.com
   ```

**Regularly Update PowerDNS:**

Keeping PowerDNS updated ensures that you are protected from known vulnerabilities. Regularly check for updates:

```bash
sudo apt update && sudo apt upgrade
```

---

## **Automating DNS Tasks with Scripting**

**Automating DNS Record Management:**

Automation helps manage DNS records efficiently, especially in environments with multiple domains or frequent changes.

**Example Script to Add A Records:**

The following script adds A records for multiple subdomains using SQLite:

```bash
#!/bin/bash

DOMAIN="example.com"
IP_ADDRESS="192.168.1.100"
SUBDOMAINS=("www" "mail" "ftp")

for SUB in "${SUBDOMAINS[@]}"; do
    sudo sqlite3 /var/lib/powerdns/pdns.sqlite3 "
    INSERT INTO records (domain_id, name, content, type, ttl) 
    VALUES (
        (SELECT id FROM domains WHERE name='$DOMAIN'), 
        '$SUB.$DOMAIN', 
        '$IP_ADDRESS', 
        'A', 
        3600
    );"
    echo "Added A record for $SUB.$DOMAIN"
done
```

**Breakdown:**

- **`DOMAIN="example.com"`**: The primary domain for the DNS records.
- **`IP_ADDRESS="192.168.1.100"`**: The IP address associated with the subdomains.
- **`SUBDOMAINS=("www" "mail" "ftp")`**: An array of subdomains to be added.
- **`sudo sqlite3 /var/lib/powerdns/pdns.sqlite3`**: Executes the SQL command to insert records into the SQLite database.

---

## **Troubleshooting Common DNS Issues**

**Issue 1: DNS Records Not Resolving**

**Symptoms:** DNS records are not resolving, or clients receive outdated information.

**Troubleshooting Steps:**

1. **Check DNS Propagation:**

   Use the `dig` command to check DNS record propagation:

   ```bash
   dig www.example.com @8.8.8.8
   ```

2. **Verify Zone Configuration:**

   Ensure that the zone is correctly configured in the SQLite database:

   ```bash
   sudo -u pdns sqlite3 /var/lib/powerdns/pdns.sqlite3 "SELECT * FROM domains WHERE name='example.com';"
   ```

   Check that all necessary records are present:

   ```bash
   sudo -u pdns sqlite3 /var/lib/powerdns/pdns.sqlite3 "SELECT * FROM records WHERE domain_id=(SELECT id FROM domains WHERE name='example.com');"
   ```

3. **Check PowerDNS Logs:**

   Review PowerDNS logs for any errors or warnings:

   ```bash
   sudo tail -f /var/log/syslog | grep pdns
   ```

**Issue 2: Zone Transfer Failures**

**Symptoms:** Zone transfers between primary and secondary DNS servers are failing.

**Troubleshooting Steps:**

1. **Check Zone Transfer Settings:**

   Verify that the `allow-axfr-ips` directive includes the correct IP addresses.

2. **Verify Network Connectivity:**

   Ensure that the DNS servers can communicate:

   ```bash
   ping 192.168.1.2
   ```

3. **Check Firewall Rules:**

   Confirm that your firewall allows DNS traffic (port 53) between the servers:

   ```bash
   sudo ufw allow from 192.168.1.2 to any port 53
   ```

---

## **References and Further Reading**

- **PowerDNS Documentation:** [PowerDNS Official Documentation](https://doc.powerdns.com/)
- **DNS Security Best Practices:** [DNS Security (DNSSEC)](https://www.iana.org/dnssec)
- **SQLite Documentation:** [SQLite Official Documentation](https://www.sqlite.org/docs.html)
- **Ubuntu 20.04 DNS Server Setup:** [DigitalOcean: How to Set Up PowerDNS on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-powerdns-on-ubuntu-20-04)

---
