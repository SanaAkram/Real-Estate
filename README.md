i # Real Estate Classification API Configuration Guide

Welcome to the Real Estate Classification API Configuration Guide! This comprehensive guide will assist you in setting up the Real Estate Classification API on your Ubuntu server. Ensure to follow each step diligently for a smooth installation process.

## Table of Contents

1. [Prerequisites](#prerequisites)
   - [Hardware Requirements](#hardware-requirements)
   - [Software Requirements](#software-requirements)
2. [Installing MySQL](#installing-mysql)
   - [Configuring MySQL](#configuring-mysql)
   - [Verifying MySQL Installation](#verifying-mysql-installation)
3. [Setting Up and Testing SSH Keys with GitHub](#setting-up-and-testing-ssh-keys-with-github)
4. [Installing Python 3.6 on Ubuntu](#installing-python-36-on-ubuntu)
   - [Conclusion](#conclusion)
5. [Installing Components from Ubuntu Repositories](#installing-components-from-ubuntu-repositories)
6. [Creating Python Virtual Environments](#creating-python-virtual-environments)
7. [Downloading Machine Learning Models](#downloading-machine-learning-models)
8. [Install NVIDIA Drivers and CUDA Toolkit](#install-nvidia-drivers-and-cuda-toolkit)

## 1. Prerequisites <a name="prerequisites"></a>

Before initiating the installation process, ensure your system meets the following prerequisites:

### Hardware Requirements <a name="hardware-requirements"></a>

- RAM: 14-16GB
- Hard Disk: 40-60GB
- GPU Memory: 4-15GB

### Software Requirements <a name="software-requirements"></a>

- NVIDIA Driver
- CUDA 10.0
- CuDNN
- MySQL 5.5
- Update `max_connections` value to 500 in MySQL

## 2. Installing MySQL <a name="installing-mysql"></a>

To install MySQL, execute the following command:

```bash
sudo apt-get install mysql-server
```

Follow the on-screen prompts to set a root password for MySQL.

### Configuring MySQL <a name="configuring-mysql"></a>

After installation, adjust MySQL's configuration by updating the `max_connections` value. Open the MySQL configuration file:

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Find `max_connections` and set it to `500`.

### Verifying MySQL Installation <a name="verifying-mysql-installation"></a>

Check if MySQL server is running:

```bash
systemctl status mysql
```

Continue formatting and adding content for the remaining sections as needed. This structure provides a clear and organized guide for users to follow.

Sure, let's continue completing the readme:

## 3. Setting Up and Testing SSH Keys with GitHub <a name="setting-up-and-testing-ssh-keys-with-github"></a>

This section outlines the process for generating a new SSH key, adding it to a GitHub account, and testing the SSH connection to GitHub for secure, password-less interaction with GitHub repositories over SSH.

### Prerequisites

- Access to a terminal on a Linux-based system (e.g., Ubuntu)
- A GitHub account

### Steps

1. **Generating an SSH Key**

   Begin by generating a new SSH key pair using the `ssh-keygen` command. The key will be secured with a passphrase for additional security.

   ```bash
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```

   When prompted, enter the filename to save the key, or press Enter to use the default location (`~/.ssh/id_rsa`).

2. **Starting the SSH Agent**

   Start the SSH agent in the background to manage your keys.

   ```bash
   eval "$(ssh-agent -s)"
   ```

3. **Adding Your SSH Key to the SSH Agent**

   Add your SSH private key to the `ssh-agent`. Replace `id_rsa` with your filename if you used a custom one.

   ```bash
   ssh-add ~/.ssh/id_rsa
   ```

4. **Adding Your SSH Key to GitHub**

   - Copy the content of your public SSH key file. Replace `id_rsa.pub` with your filename if you used a custom one.

     ```bash
     cat ~/.ssh/id_rsa.pub
     ```

   - Log in to your GitHub account, navigate to **Settings** > **SSH and GPG keys** > **New SSH key**, and paste your key into the field. Provide a descriptive title and click **Add SSH Key**.

5. **Testing Your SSH Connection**

   Finally, test your SSH connection to GitHub. You should receive a success message acknowledging your GitHub username.

   ```bash
   ssh -T git@github.com
   ```

   If successful, you'll see a message like:

   ```plaintext
   Hi {username}! You've successfully authenticated, but GitHub does not provide shell access.
   ```


## 4. Installing Python 3.6 on Ubuntu <a name="installing-python-36-on-ubuntu"></a>

This guide will walk you through the steps to install Python 3.6 on an Ubuntu system using the `deadsnakes` Personal Package Archive (PPA).

### Prerequisites

- Access to a terminal on an Ubuntu system.
- Permission to install software on the system.

### Steps

1. **Add the `deadsnakes` PPA**

   Open a terminal and run the following command to add the `deadsnakes` PPA to your system:

   ```bash
   sudo add-apt-repository ppa:deadsnakes/ppa
   ```

2. **Update Package Index**

   Update the package index to ensure your system knows about the packages available in the newly added PPA:

   ```bash
   sudo apt update
   ```

3. **Install Python 3.6**

   Once the package index is updated, install Python 3.6 using the `apt` package manager:

   ```bash
   sudo apt install python3.6
   ```

4. **Verify Installation**

   After installation, verify that Python 3.6 has been installed successfully by running:

   ```bash
   python3.6 --version
   ```

   This command should output the version of Python 3.6 installed on your system.

## 5. Installing Components from Ubuntu Repositories <a name="installing-components-from-ubuntu-repositories"></a>

Our first step will be to install all the necessary components from the Ubuntu repositories to build our Python environment. These include `python3-pip`, along with other packages and development tools necessary for a robust programming environment.

```bash
sudo apt update
sudo apt install python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools
```

## 6. Creating Python Virtual Environments <a name="creating-python-virtual-environments"></a>

Next, we'll set up virtual environments to isolate our Flask application from other Python files on the system.

Start by installing the `python3-venv` package to install the `venv` module:

```bash
sudo apt install python3-venv
```

Then, create virtual environments for your project:

```bash
python3.6 -m venv venv_server
python3.6 -m venv venv_web
python3.6 -m venv venv_api
```

Activate each environment and install the required packages:

```bash
source venv_server/bin/activate
pip install -r server_requirements.txt
deactivate

source venv_web/bin/activate
pip install -r web_requirements.txt
deactivate

source venv_api/bin/activate
pip install -r api_requirements.txt
deactivate
```

## 7. Downloading Machine Learning Models <a name="downloading-machine-learning-models"></a>

To include machine learning models in your project, follow these steps:

### Old Version

```bash
cd old_version/batch_api_code/kavlibs
wget https://www.dropbox.com/s/ohs0fwb83o5p4ic/old_models.zip
unzip old_models.zip
```

### Updated Version

```bash
cd updated_version/batch_api_code_modified/kavlibs
wget https://www.dropbox.com/s/uu32bt4qfjfcfdf/models.zip
unzip models.zip
cd ../..
cd batch_api_code_modified_2/kavlibs
wget https://www.dropbox.com/s/uu32bt4qfjfcfdf/models.zip
unzip models.zip
cd ../../../..
```

## 8. Install NVIDIA Drivers and CUDA Toolkit <a name="install-nvidia-drivers-and-cuda-toolkit"></a>

### Checking Server Specifications

Use the `lshw` command to check GPU and determine the NVIDIA driver currently installed on your system:

```bash
sudo lshw -C display
```
*If not then contact your manager.


## 8. Install NVIDIA Drivers and CUDA Toolkit <a name="install-nvidia-drivers-and-cuda-toolkit"></a>

### Installing NVIDIA Drivers and CUDA Toolkit

To install NVIDIA drivers and CUDA Toolkit, follow these steps:

1. **Install NVIDIA drivers**

   Run the following commands to install NVIDIA drivers:

   ```bash
   sudo apt install nvidia-headless-535-server nvidia-utils-535-server -y
   sudo apt install nvidia-driver-535
   ```

2. **Download and install NVIDIA driver**

   Download and install the NVIDIA driver by executing the following commands:

   ```bash
   sudo wget https://us.download.nvidia.com/tesla/440.95.01/NVIDIA-Linux-x86_64-440.95.01.run
   sudo sh NVIDIA-Linux-x86_64-440.95.01.run
   ```

   Make sure to replace the URL with the appropriate NVIDIA driver version for your system.

3. **Install CUDA Toolkit 10.0**

   Download and install CUDA Toolkit 10.0 with the following commands:

   ```bash
   sudo wget https://developer.nvidia.com/compute/cuda/10.0/Prod/local_installers/cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb
   sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb
   sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
   sudo apt-get update
   sudo apt -y install cuda-10-0
   ```

   Replace `<version>` in the `apt-key add` command with the appropriate CUDA repository version.

4. **Add CUDA binaries to PATH and library path**

   Add CUDA binaries to PATH and library path by running:

   ```bash
   export PATH=/usr/local/cuda-10.0/bin${PATH:+:${PATH}}
   export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
   ```

5. **Install cuDNN 7.5.0**

   Download and install cuDNN 7.5.0 with the following commands:

   ```bash
   sudo wget https://www.dropbox.com/scl/fi/8fmpwmxun8ebsrtlw5an6/libcudnn7_7.5.0.56-1-cuda10.0_amd64.deb?rlkey=7fnj43qq6544eufcq7jijq4lc&st=yuz87m80&dl=0 -O libcudnn7_7.5.0.56-1+cuda10.0_amd64.deb
   sudo dpkg -i libcudnn7_7.5.0.56-1+cuda10.0_amd64.deb
   sudo apt-get -y install cudnn
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

Ensure that the `nvcc` command outputs the version of CUDA installed on your system.


```

