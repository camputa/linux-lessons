# Practical Guide: Mastering Netplan and Configuring Ubuntu IP Addresses

## Introduction

**Purpose:**
Hey Team! Today, we’re diving into Netplan, a powerful and simple-to-use utility for configuring network interfaces in Ubuntu. Networking can seem complex, but with Netplan, it’s more straightforward than you think. By mastering this tool, you'll be able to set up, modify, and troubleshoot network configurations with ease.

**Objective:**
Our objective is to understand how to use Netplan to configure IP addresses on Ubuntu. We will cover how to set up both static and dynamic IP addresses, apply the configuration, and verify the network settings. By the end of this guide, you'll be equipped to handle network configuration tasks confidently.

**Key Learning Outcomes:**

- Grasp the fundamentals of Netplan and its role in network configuration
- Learn how to set up and apply network configurations using Netplan
- Understand the difference between static and dynamic IP addresses
- Gain the ability to troubleshoot and verify network settings

---

## Let's Get Started!

### Understanding Netplan

Netplan is a utility in Ubuntu that uses YAML descriptions to configure network interfaces. It simplifies the process of defining network settings, replacing older methods like `/etc/network/interfaces`.

**Netplan Configuration Files:**

- Netplan configuration files are stored in `/etc/netplan/`.
- They have the `.yaml` extension and can be edited with any text editor.

### Checking Current Network Configuration

Before making changes, it's useful to understand the current network setup.

**Steps:**
1. Open your terminal.
2. Display current IP configuration:

    ```bash
    ip addr show
    ```

    This command shows the current IP addresses assigned to your network interfaces.

3. Display routing table:

    ```bash
    ip route show
    ```

### Editing Netplan Configuration

Let’s dive into editing Netplan configuration to set a static IP address.

**Steps:**

1. Open the Netplan configuration file in your preferred text editor (e.g., `nano`, `vim`):

    ```bash
    sudo nano /etc/netplan/01-netcfg.yaml
    ```

2. Configure a static IP address. Here’s a sample configuration:

    ```yaml
    network:
      version: 2
      ethernets:
        eth0:
          dhcp4: no
          addresses: [192.168.1.10/24]
          gateway4: 192.168.1.1
          nameservers:
            addresses: [8.8.8.8, 8.8.4.4]
    ```

    - `dhcp4: no` disables DHCP and allows you to set a static IP.
    - `addresses` specifies the static IP address and subnet mask.
    - `gateway4` sets the default gateway.
    - `nameservers` lists DNS servers.

3. Save and exit the text editor.

### Applying the Netplan Configuration

After editing the configuration file, you need to apply the changes.

**Steps:**

1. Apply the Netplan configuration:

    ```bash
    sudo netplan apply
    ```

2. Verify the new IP configuration:

    ```bash
    ip addr show
    ```

### Configuring a Dynamic IP Address

If you prefer to use DHCP to automatically obtain an IP address, here’s how to configure it.

**Steps:**

1. Open the Netplan configuration file:

    ```bash
    sudo nano /etc/netplan/01-netcfg.yaml
    ```

2. Set DHCP to `yes`:

    ```yaml
    network:
      version: 2
      ethernets:
        eth0:
          dhcp4: yes
    ```

3. Save and exit the text editor.

4. Apply the Netplan configuration:

    ```bash
    sudo netplan apply
    ```

5. Verify the IP configuration:

    ```bash
    ip addr show
    ```

### Troubleshooting and Verification

It’s important to ensure your configuration works as expected. Here are some commands to help you troubleshoot and verify:

**Common Commands and Options:**

- Check the status of network interfaces:

    ```bash
    ip link show
    ```

- Verify DNS resolution:

    ```bash
    nslookup google.com
    ```

- Test network connectivity:

    ```bash
    ping 8.8.8.8
    ```

- View the systemd network logs for detailed troubleshooting:

    ```bash
    journalctl -u systemd-networkd
    ```

## Practice Tutorial: Configuring a Static IP Address

**Objective:** Practice configuring a static IP address using Netplan on a Ubuntu system.

1. **Edit Netplan Configuration:**
    - Open the Netplan configuration file:

      ```bash
      sudo nano /etc/netplan/01-netcfg.yaml
      ```

    - Add the following configuration:

      ```yaml
      network:
        version: 2
        ethernets:
          eth0:
            dhcp4: no
            addresses: [192.168.1.100/24]
            gateway4: 192.168.1.1
            nameservers:
              addresses: [8.8.8.8, 8.8.4.4]
      ```

    - Save and exit the text editor.

2. **Apply the Configuration:**
    - Apply the changes:

      ```bash
      sudo netplan apply
      ```

3. **Verify the Configuration:**
    - Check the IP configuration:

      ```bash
      ip addr show
      ```

    - Ping the gateway to ensure connectivity:

      ```bash
      ping 192.168.1.1
      ```

---

## Summary

Awesome job, team! You've now got the skills to configure network interfaces using Netplan on Ubuntu. This essential knowledge helps ensure our servers are properly configured and connected, providing a solid foundation for all our development and deployment activities.

Remember, networking is a critical aspect of system administration and development. By mastering tools like Netplan, you're not just learning new commands—you're building the skills to create robust, reliable, and secure networked systems. Keep experimenting, stay curious, and let's continue to elevate our technical prowess together!
