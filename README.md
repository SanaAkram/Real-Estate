# Installation Guide: Real Estate Classification API

The following guide will walk you through the process of setting up the Real Estate Classification API on an Ubuntu server. This guide assumes you have access to a server with Ubuntu installed.

## Prerequisites

Before starting the installation process, ensure you have the following prerequisites:

### Hardware Requirements

- RAM: 14-16GB
- Hard Disk: 40-60GB
- GPU Memory: 4-15GB

### Software Requirements

- NVIDIA Driver
- CUDA 
- CuDNN
- MySQL 5.5
- Update `max_connections` value to 500 in MySQL

### Additional Libraries (Ubuntu)

- Libsvm3
- Python-libsvm
### Installing MySQL

```bash
sudo apt-get install mysql-server
```

During the installation process, you'll be prompted to set a root password for MySQL.

### Configuring MySQL

After installation, adjust MySQL's configuration by updating the `max_connections` value. Open the MySQL configuration file using a text editor:

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Find the `max_connections` parameter and set it to `500`:

```
max_connections = 500
```

Save the file and exit the text editor.

### Verifying MySQL Installation

Check if MySQL server is running:

```bash
systemctl status mysql
```

You should see output indicating that MySQL is active and running.


# Setting Up and Testing SSH Keys with GitHub

This document outlines the process for generating a new SSH key, adding it to a GitHub account, and testing the SSH connection to GitHub. This setup is crucial for secure, password-less interaction with GitHub repositories over SSH.

## Prerequisites

- Access to a terminal on a Linux-based system (e.g., Ubuntu)
- A GitHub account

## Steps

### 1. Generating an SSH Key

First, generate a new SSH key pair using the `ssh-keygen` command. The key is secured with a passphrase for additional security.

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

When prompted, enter the filename to save the key if you want to use a specific name or location; otherwise, you can press Enter to use the default location (`~/.ssh/id_rsa`).

### 2. Starting the SSH Agent

Start the SSH agent in the background to manage your keys.

```bash
eval "$(ssh-agent -s)"
```

### 3. Adding Your SSH Key to the SSH Agent

Add your SSH private key to the `ssh-agent`. If you've used a custom filename, replace `id_rsa` with your filename.

```bash
ssh-add ~/.ssh/id_rsa
```

### 4. Adding Your SSH Key to GitHub

- Copy the content of your public SSH key file. If you've used a custom filename, replace `id_rsa.pub` with your filename.

  ```bash
  cat ~/.ssh/id_rsa.pub
  ```

- Log in to your GitHub account, go to **Settings** > **SSH and GPG keys** > **New SSH key**, and paste your key into the field. Provide a descriptive title and click **Add SSH Key**.

### 5. Testing Your SSH Connection

Finally, test your SSH connection to GitHub. You should receive a success message acknowledging your GitHub username.

```bash
ssh -T git@github.com
```

If successful, you'll see a message like:

```plaintext
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

## Step 2: Install Python 3.9 and Create Virtual Environment

1. Install Python 3.9:
   ```
   sudo apt update
   sudo apt install python3.9
   ```
   #### Checking Python Version
   
   After installing dependencies and setting up the environment, verify the Python version:
   
   ```bash
   python --version
   ```

Ensure that Python 3.9 is displayed as the installed version.

2. Activate Python 3.9:
   ```
   sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.9 1
   ```

3. Create a virtual environment for Python 3.9 into project directory:
   ```
   python3.9 -m venv venv_3.9
   ```

4. Activate the virtual environment:
   ```
   source venv_3.9/bin/activate
   ```

## Step 3: Install Dependencies

1. Install project dependencies from requirements.txt using following command:
   ```
   pip install -r requirements.txt
   ```

## Step 4: Install NVIDIA Drivers and CUDA Toolkit

### Checking Server Specifications

Use the `lshw` command to check GPU and determine the NVIDIA driver currently installed on your system:

```bash
sudo lshw -C display
```

Identify your GPU model from the output, and note the installed NVIDIA driver version.

### Installing NVIDIA Drivers and CUDA Toolkit

Install NVIDIA drivers and CUDA Toolkit according to server specifications. For example, if your GPU is NVIDIA Tesla T4 and requires CUDA 11.x compatibility:

```bash
sudo apt install nvidia-driver-version

# Install CUDA Toolkit 11.x
sudo apt install nvidia-cuda-toolkit
```

Replace `'nvidia-driver-version'` with the appropriate NVIDIA driver version based on your server specifications.

### Verifying NVIDIA Driver Installation

After installing the NVIDIA driver, verify its installation using `nvidia-smi`:

```bash
nvidia-smi
```

You should see information about your NVIDIA GPU, confirming that the driver is installed correctly.

### Verifying CUDA Installation

After installing the NVIDIA driver and CUDA Toolkit, verify CUDA installation:

```bash
nvcc --version
```

You should see output confirming the installed CUDA version.


With these instructions added, users will be guided through checking server specifications, installing the appropriate NVIDIA drivers and CUDA Toolkit, and verifying the installation to ensure compatibility and functionality.

