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
```
* Update max_connections value to 500 in MySQL. Login to your MySQL terminal with the privileged user and execute the following query.
``` 
mysql> SET GLOBAL max_connections = 500;
```

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
Hi {username}! You've successfully authenticated, but GitHub does not provide shell access.
```

### Step 2: Installing Python 3.6 on Ubuntu

This guide will walk you through the steps to install Python 3.6 on an Ubuntu system using the `deadsnakes` Personal Package Archive (PPA).

## Prerequisites

- Access to a terminal on an Ubuntu system.
- Permission to install software on the system.

## Steps

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

## Conclusion

You've successfully installed Python 3.6 on your Ubuntu system using the `deadsnakes` PPA. You can now use Python 3.6 for 

* Additional Libraries to be installed (Ubuntu):
```
Libsvm3 (sudo apt install libsvm3)
Python-libsvm (sudo apt install python-libsvm)
```

## Step 1 — Installing the Components from the Ubuntu Repositories
Our first step will be to install all of the pieces that we need from the Ubuntu repositories. We will install pip, the Python package manager, to manage our Python components. We will also get the Python development files necessary to build uWSGI.

First, let's update the local package index and install the packages that will allow us to build our Python environment. These will include python3-pip, along with a few more packages and development tools necessary for a robust programming environment:

```
sudo apt update
sudo apt install python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools
```
With these packages in place, let’s move on to placing files for our project.

you can check what we are going to achieve [here](https://github.com/Ali-Tahir/real_estate_classification_api/blob/master/docs/mechanism.pdf)


## Step 2 — Creating Python Virtual Environments
Next, we’ll set up virtual environments in order to isolate our Flask application from the other Python files on the system.

Start by installing the python3-venv package, which will install the venv module:
```
sudo apt install python3-venv
```

First, let’s install wheel with the local instance of pip to ensure that our packages will install even if they are missing wheel archives:
```
pip install wheel
```
Now we will create our virtual environments (assuming you are in **real_estate_classification_api** directory)
```
python3.6 -m venv venv_server
python3.6 -m venv venv_web
python3.6 -m venv venv_api
```

Now make sure you are in **real_estate_classification_api** directory and run following commands one by one to setup the environments with required packages
```
venv_server/bin/pip install -r server_requirements.txt
venv_web/bin/pip install -r web_requirements.txt
venv_api/bin/pip install -r api_requirements.txt
```


Now, to place our machine learning models first we need to install unzip so we could extract our models later from downloaded zip files!

```
sudo apt-get install unzip
```

* ##### Old version

	Move to the old version models directory using following command!

	```
	cd old_version/batch_api_code/kavlibs
	```

	Now we must include our models!

	```
	wget https://www.dropbox.com/s/ohs0fwb83o5p4ic/old_models.zip
	unzip old_models.zip
	```

* #####  Updated version

	Move to the updated version models directory by using following command!

	```
	cd updated_version/batch_api_code_modified/kavlibs
	```

	Now we must include our models!

	```
	wget https://www.dropbox.com/s/uu32bt4qfjfcfdf/models.zip
	unzip models.zip
	cd ..
	cd ..
	cd batch_api_code_modified_2/kavlibs
	wget https://www.dropbox.com/s/uu32bt4qfjfcfdf/models.zip
	unzip models.zip
	```

	Move back to the main **real_estate_classification_api** directory by using the following command more than once!

	```
	cd ../..
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

