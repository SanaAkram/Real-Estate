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

2. Activate Python 3.9:
   ```
   sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.9 1
   ```

3. Create a virtual environment for Python 3.9:
   ```
   python3.9 -m venv venv_3.9
   ```

4. Activate the virtual environment:
   ```
   source venv_3.9/bin/activate
   ```

## Step 3: Install Dependencies

1. Install project dependencies from requirements.txt:
   ```
   pip install -r requirements.txt
   ```

## Step 4: Install NVIDIA Drivers and CUDA Toolkit

1. Check server specifications to determine compatible NVIDIA drivers and CUDA Toolkit version.

2. Install NVIDIA drivers and CUDA Toolkit according to server specifications.

3. Verify CUDA installation:
   ```
   nvcc --version
   ```

## Step 5: Configure Database and Environment Variables

1. Update database configurations in relevant files.

2. Set environment variables as required.

## Step 6: Run API and Web Servers

1. Activate the appropriate virtual environment:
   ```
   source venv_api/bin/activate
   ```

2. Run the API server:
   ```
   python batch_api_quick_resp.py
   ```

3. Activate the virtual environment for the web server:
   ```
   source venv_web/bin/activate
   ```

4. Run the web server:
   ```
   python main.py
   ```

## Step 7: Create Systemd Unit Files and Nginx Configuration

1. Create systemd unit files for API and web servers.

2. Configure Nginx to proxy requests to the uWSGI servers.

3. Enable and start the systemd services.

4. Test the servers and Nginx configuration.

## Conclusion

You have successfully installed and configured the Real Estate Classification API on your Ubuntu server.

---

This guide covers the entire setup process from cloning the repository to configuring servers and proxies. Adjust the paths and configurations as necessary based on your specific project requirements and server setup.
