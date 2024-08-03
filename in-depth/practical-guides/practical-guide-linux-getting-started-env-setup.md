# Practical Guide: Setting Up Your Dev Environment to Experiment with Linux
 
Hey team! Today, we're diving into the exciting world of setting up a development environment to experiment with Linux. This hands-on guide will walk you through the process of installing essential tools, configuring a virtual environment, and performing basic operations within a Linux VM. This setup will be your playground for mastering Linux skills in a safe, controlled environment.

Our objective is to get you comfortable with setting up a development environment using VirtualBox, Vagrant, and Git SCM. By the end of this guide, you'll have a running Linux VM, know how to interact with it via SSH, and be able to perform basic file operations. This setup will serve as your sandbox for learning and experimentation.

**Key Learning Outcomes:**

- Install and configure VirtualBox and Vagrant
- Clone a Git repository containing a Vagrantfile
- Launch a Vagrant machine and SSH into it
- Generate SSH keys and configure SSH login
- Add a custom sudo user
- Perform basic file operations within the VM

---

## Let's Get Started!

### 1. Install VirtualBox

VirtualBox is a powerful x86 and AMD64/Intel64 virtualization product for enterprise and home use.

**Steps:**

1. Go to the [VirtualBox download page](https://www.virtualbox.org/wiki/Downloads).
2. Download the appropriate version for your operating system (Windows, macOS, Linux).
3. Run the installer and follow the on-screen instructions.

### 2. Install Vagrant

Vagrant is a tool for building and managing virtual machine environments in a single workflow.

**Steps:**

1. Go to the [Vagrant download page](https://www.vagrantup.com/downloads).
2. Download the appropriate version for your operating system.
3. Run the installer and follow the on-screen instructions.

### 3. Install Git SCM

Git SCM is a free and open-source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

**Steps:**

1. Go to the [Git SCM download page](https://git-scm.com/downloads).
2. Download the appropriate version for your operating system.
3. Run the installer and follow the on-screen instructions.

### 4. Open Git Bash Terminal

Git Bash provides a bash emulation used to run Git from the command line on Windows. For macOS or Linux, you can use the default terminal.

**Steps:**

1. Open Git Bash (Windows) or your default terminal (macOS/Linux).

### 5. Clone the Onboarding Repository

We have a repository called `linux-skills.git` that contains a Vagrantfile with an Ubuntu 20.04 base box.

**Steps:**

1. In your terminal, navigate to the directory where you want to clone the repository.
2. Run the following command to clone the repository:

    ```bash
    git clone https://github.com/yourorganization/linux-skills.git
    ```

3. Navigate into the cloned repository:

    ```bash
    cd linux-skills
    ```

### 6. Launch the Vagrant Machine

The Vagrantfile in the repository sets up a virtual machine with Ubuntu 20.04.

**Steps:**

1. In the terminal, run the following command to start the Vagrant machine:

    ```bash
    vagrant up
    ```

2. Once the machine is up and running, SSH into it using the IP address 192.168.56.30:

    ```bash
    vagrant ssh
    ```

### 7. Setup SSH Login Using `ssh-keygen`

SSH keys provide a more secure way of logging into a server with SSH than using a password alone.

**Steps:**

1. On your local machine, generate a new SSH key pair:

    ```bash
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    ```

    Follow the prompts to save the key pair (default locations are usually fine).
2. Copy the public key to the Vagrant machine:

    ```bash
    vagrant ssh
    mkdir -p ~/.ssh
    echo "YOUR_PUBLIC_KEY" >> ~/.ssh/authorized_keys
    chmod 600 ~/.ssh/authorized_keys
    ```

### 8. Add a Custom Sudo Username

Adding a custom sudo user allows for better management and control over the system.

**Steps:**

1. SSH into the Vagrant machine:

    ```bash
    vagrant ssh
    ```

2. Create a new user with sudo privileges:

    ```bash
    sudo adduser your_custom_username
    sudo usermod -aG sudo your_custom_username
    ```

### 9. Add Your Name to a Text File Using `cat`

The `cat` command is used to create or display the contents of files.

**Steps:**

1. Use `cat` to add your name to a text file:

    ```bash
    echo "Your Name" | sudo tee -a /var/www/html/dev-team.txt
    ```

2. Verify the contents of the file:

    ```bash
    cat /var/www/html/dev-team.txt
    ```

---

## Summary

Congratulations, team! You've successfully set up your development environment and performed essential tasks using Linux commands. This guide serves as a foundation for your ongoing learning and experimentation. Keep practicing, stay curious, and remember: every expert was once a beginner. Together, we're building a strong, skilled, and confident team. Happy coding!
