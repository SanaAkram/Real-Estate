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

...

This completes the comprehensive setup guide for the Real Estate Classification API. Following these instructions will ensure a smooth installation process and proper functioning of the API. If you need further assistance, refer to the linked resources or reach out for support.
