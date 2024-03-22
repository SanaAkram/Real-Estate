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
- CUDA 9.0 / 10.0 (from Archive)
- CuDNN
- MySQL 5.5
- Update `max_connections` value to 500 in MySQL

### Additional Libraries (Ubuntu)

- Libsvm3
- Python-libsvm

## Step 1: Setup SSH Key and Clone Repository

1. Generate an SSH key on your local machine if you haven't already:
   ```
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```

2. Add the SSH key to your GitHub account.

3. Install Git on your local machine:
   ```
   sudo apt-get install git-core
   ```

4. Clone the repository using SSH:
   ```
   git clone git@github.com:username/repository.git
   ```
## Step 2: Install Python 3.9 and Create Virtual Environment

1. Install Python 3.9:
   ```
   sudo apt update
   sudo apt install python3.9
   ```
   # Checking Python Version
   
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

