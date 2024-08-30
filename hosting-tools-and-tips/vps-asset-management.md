# **VPS Asset Management Document**

---

## **1. General VPS Information**

**Description:**
This section provides a detailed overview of the VPS server hosted on AWS, highlighting its key specifications, technical attributes, and scalability options. The VPS is designed for efficient email hosting across multiple domains with potential for future upgrades.

**Details:**
- **VPS Server Name:** `email-server-01`
- **Hosting Provider:** AWS (Amazon Web Services)
- **Instance Type:** `t3a.medium` (Scalable to `t3a.large` as needed)
- **Operating System:** Ubuntu 20.04 LTS
- **CPU:** 2 vCPUs (Upgradeable to 4 vCPUs)
- **RAM:** 8 GB (Expandable to 16 GB)
- **Storage:** 50 GB SSD (Additional volumes can be added)
- **Purchase Date:** `2024-07-29`
- **IP Address:** `192.0.2.10`
- **Additional IPs:** (For future scaling)
- **Region:** `us-east-1`
- **Security Groups:** `email-server-sg` (Allow SMTP, IMAP, HTTPS, SSH)
- **Elastic IP:** `52.10.10.10`

**Scalability:**
- Plan for increasing storage, adding additional IPs, and upgrading instance type based on traffic and client growth.

---

## **2. Hosting Subscriptions**

**Description:**
Details the current hosting subscription plan, including domains hosted, billing cycle, and pricing structure. This section also considers future subscription expansions as client needs evolve.

**Details:**
- **Subscription Name:** `Email Hosting - Standard Plan`
- **Domains Hosted:** `a-domain.com, b-domain.com, c-domain.com`
- **Billing Cycle:** Monthly
- **Price:** $50/month (Discounts available for annual payments)
- **VPS Server ID:** `email-server-01`
- **Future Subscription Plans:** Options for adding more domains or upgrading to a premium plan with advanced features.

---

## **3. Email Server Configuration**

**Description:**
Covers the configuration of the email server, focusing on software, security, and customization. This section also highlights future-proofing strategies for increasing email server capacity and integrating with other services.

**Details:**
- **MTA (Mail Transfer Agent):** Postfix (Configured for high deliverability)
- **IMAP Server:** Dovecot (Secure IMAP with SSL/TLS encryption)
- **Webmail Client:** Roundcube (Customizable interface)
- **Email Ports Open:**
  - SMTP: 25 (with submission port 587 for client emails)
  - IMAP: 143, IMAPS: 993
  - HTTP: 80, HTTPS: 443
- **SSL Certificate Provider:** Let's Encrypt (Automatic renewal configured)
- **SSL Expiry Date:** `2025-07-29`
- **Advanced Security:** Consider implementing DKIM, DMARC, and SPF records for enhanced email security.

---

## **4. Domains & SSL Certificates**

**Description:**
Lists the domains hosted on the VPS, associated SSL certificates, and key client information. This section ensures that all domains are secure and compliant with industry standards.

**Details:**
- **Domain Name:** `a-domain.com`
  - **SSL Certificate:** Let's Encrypt
  - **Expiry Date:** `2025-07-29`
  - **Hosting Subscription:** `Email Hosting`
  - **Client Name:** Client A
  - **Industry:** Tech
  - **Contact Details:** `clientA@example.com`

- **Domain Name:** `b-domain.com`
  - **SSL Certificate:** Let's Encrypt
  - **Expiry Date:** `2025-07-29`
  - **Hosting Subscription:** `Email Hosting`
  - **Client Name:** Client B
  - **Industry:** Marketing
  - **Contact Details:** `clientB@example.com`

- **Domain Name:** `c-domain.com`
  - **SSL Certificate:** Let's Encrypt
  - **Expiry Date:** `2025-07-29`
  - **Hosting Subscription:** `Email Hosting`
  - **Client Name:** Client C
  - **Industry:** Education
  - **Contact Details:** `clientC@example.com`

**Compliance and Renewal:**
- Regularly audit SSL certificates and domain registrations to ensure timely renewals and compliance with security standards.

---

## **5. Security & Backup**

**Description:**
Outlines the security measures and backup strategies implemented on the VPS to protect data and maintain service continuity. This section includes advanced security measures and backup protocols to minimize downtime and data loss.

**Details:**
- **Firewall:** UFW (Uncomplicated Firewall) configured with strict rules
- **Security Updates:** Automatic Weekly Updates (With a manual review process)
- **Backup Solution:** AWS S3 (Daily Backups with versioning)
- **Backup Frequency:** Daily backups with weekly snapshots
- **Disaster Recovery Plan:** Regular testing, off-site storage, and documented recovery procedures
- **Data Retention Policy:** 30 Days (With options for extended retention for critical data)
- **Additional Security:** Implement Intrusion Detection Systems (IDS) and regular security audits.

---

## **6. Client Details**

**Description:**
Includes detailed information about the clients hosted on this VPS, focusing on industry, contact information, and client satisfaction metrics.

**Details:**
- **Client Name:** Client A
  - **Industry:** Tech
  - **Domains Hosted:** `a-domain.com`
  - **Email Contact:** `clientA@example.com`
  - **Phone:** +1 555-123-4567

- **Client Name:** Client B
  - **Industry:** Marketing
  - **Domains Hosted:** `b-domain.com`
  - **Email Contact:** `clientB@example.com`
  - **Phone:** +1 555-987-6543

- **Client Name:** Client C
  - **Industry:** Education
  - **Domains Hosted:** `c-domain.com`
  - **Email Contact:** `clientC@example.com`
  - **Phone:** +1 555-456-7890

**Client Satisfaction:**
- Implement a feedback loop to track client satisfaction and address issues proactively.

---

## **7. Performance Monitoring & Alerts**

**Description:**
Describes the monitoring tools and alerting systems in place to ensure optimal VPS and email server performance. This section also suggests integrating automated responses for critical alerts.

**Details:**
- **CPU Usage:**
  - **Threshold:** > 80%
  - **Monitoring Tool:** CloudWatch
  - **Alert Type:** Email
  - **Contact:** `admin@example.com`

- **Disk Space Utilization:**
  - **Threshold:** > 90%
  - **Monitoring Tool:** CloudWatch
  - **Alert Type:** SMS
  - **Contact:** `+1 555-555-5555`

- **SMTP Queue Length:**
  - **Threshold:** > 1000 mails
  - **Monitoring Tool:** Custom Script
  - **Alert Type:** Email
  - **Contact:** `support@example.com`

- **SSL Certificate Expiry:**
  - **Threshold:** < 30 days
  - **Monitoring Tool:** Certbot
  - **Alert Type:** Email
  - **Contact:** `it@example.com`

**Automated Responses:**
- Consider integrating automated scripts to handle certain alerts, such as restarting services or notifying key personnel of critical issues.

---

## **8. Notes & Additional Information**

**Description:**
Provides additional notes, customization details, and any other relevant information about the VPS and email server setup.

**Details:**
- **Postfix Configuration:** Custom Postfix setup for optimized email delivery, including anti-spam measures.
- **Dovecot Configuration:** Secure IMAP setup with SSL/TLS for encrypted communication.
- **Roundcube Customization:** Branded Roundcube interface to match client needs and enhance user experience.
- **Compliance:** Ensure all setups comply with GDPR and other relevant data protection regulations.
- **Future Enhancements:** Potential upgrades or integrations, such as connecting with third-party analytics tools.
