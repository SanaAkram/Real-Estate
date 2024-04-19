# Real Estate Classification API Configuration Guide

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




#### let's first edit some configurations
DB configurations - you must have same db configurations in following given files
```
USER = "pdi"
HOST = "localhost"
PASSWORD = "Kavtech@123"
DB_NAME = 'classification_data'
If required port=3306
By default POOL_SIZE=20
```
Files to update for DB configurations:
```
real_estate_classification_api/website/db_connection.py
real_estate_classification_api/website/restart_database_update.py
real_estate_classification_api/updated_version/parallel_listing/db_connection.py
real_estate_classification_api/updated_version/parallel_listing/db_utilities.py
```

Other Path variables need to set manually in these files according to your project structure
```
real_estate_classification_api/updated_version/batch_api_code_modified/main_script.py
real_estate_classification_api/updated_version/batch_api_code_modified/uwsgi.ini
real_estate_classification_api/updated_version/batch_api_code_modified_2/main_script.py
real_estate_classification_api/updated_version/batch_api_code_modified_2/uwsgi.ini
real_estate_classification_api/updated_version/parallel_listing/uwsgi.ini
```

#### Now we can continue with our installation, first lets quickly test our API
make sure you are in **real_estate_classification_api**  directory
first we will activate our api venv **venv_api**
```
source venv_api/bin/activate
```

move to api directory **updated_version/batch_api_code_modified**
```
cd updated_version/batch_api_code_modified
```

now, lets run our classification api
```
python batch_api_quick_resp.py
```

now in browser hit the following link or provide your image after url=**your_img_url**&hybrid=1&new_source=1&score=1
```
http://localhost:4030/api/?key=AzuFhhs5fs46-SJbsg3GS22@GSFFXDSqtXElsjbzup&url=https://images.pexels.com/photos/186077/pexels-photo-186077.jpeg&hybrid=1&new_source=1&score=1
```

after that, you should see some JSON response like given below!
```
https://jsonblob.com/feb74272-53f4-11ea-a41b-8932613a04c4
```

#### Now we need to create some tmux sessions
First, we will create tmux sessions for API and server scripts so, if we log out of our ssh sessions our scripts will remain running on the backend in tmux.

use the following command in the terminal to check if tmux is working!
```
tmux
```
Install tmux if you do not have it already!
```
sudo apt install tmux
```

Now close all the running API or server scripts and use the following command to start the first API tmux session
```
tmux new -s classification_4031
```
now in this session go to the *real_estate_classification_api* directory and activate the virtual environment *venv_api*.
```
source venv_api/bin/activate
```
Now use the following command to edit the API file and to change the port to 4030 at the bottom
```
nano updated_version/batch_api_code_modified/batch_api_quick_resp.py
```

After activating the environment use following command to run the API
```
python updated_version/batch_api_code_modified/batch_api_quick_resp.py
```
Now enter the following command to detach from the Tmux session and return to your normal shell
```
Ctrl+b d
```

Now create second tmux session for our API
```
tmux new -s classification_4033
```

Now in this session go to the *real_estate_classification_api* directory and activate the virtual environment *venv_api* .

```
source venv_api/bin/activate
```

After activating the environment use following command to edit the API file and to change the port to 4032 as we can not run two scripts on the same port
```
nano updated_version/batch_api_code_modified_2/batch_api_quick_resp.py
```
Now, after changing the port we can run this second instance of our API using the following command
```
python updated_version/batch_api_code_modified_2/batch_api_quick_resp.py
```

Now again, detach from the Tmux session and return to your normal shell
```
Ctrl+b d
```
Now we have two api instances listening on both 4030 and 4032 port
##### **Note : Check your project directory and skip the following Step 3 and 4 if you have the edited files in place already!
## Step 3 — Setting Up a Flask Server Application
#### We need to setup background services for load balancing

##### Creating the WSGI Entry Point
First we will activate our server environment
```
source venv_server/bin/activate
```
You can find main_script.py in  *updated_version/batch_api_code_modified/* that we will use with wsgi
Next, let's create a file that will serve as the entry point for our application. This will tell our uWSGI server how to interact with it.
Let's call the file wsgi.py:
```
nano updated_version/batch_api_code_modified/wsgi.py 
```
In this file, let's import the Flask instance from our application and then run it:
```
from main_script import app

if __name__ == '__main__':
   app.run()

```

## Step 4 — Configuring uWSGI
Your application is now written with an entry point established. We can now move on to configuring uWSGI.

#### Creating a uWSGI Configuration File
For long-term usage. We will create a uWSGI configuration file with the relevant options for this.

Let's place that file in our project directory and call it uwsgi.ini:
```
nano updated_version/batch_api_code_modified/uwsgi.ini
```
copy the below content to uwsgi.ini file and also adjust the required paths 
```
[uwsgi]
# placeholders that you have to change
my_app_folder = /home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified
my_user = pdi

chdir = %(my_app_folder)
socket = %(my_app_folder)/first_api.sock
#socket = first_api.sock
#chdir = %(my_app_folder)
file = wsgi.py
callable = app
#callable = flaskapp:app
#module = wsgi:app
# environment variables
env = CUDA_VISIBLE_DEVICES=-1
#env = PYTHONPATH=%(my_app_folder):$PYTHONPATH

master = true
processes = 5
# allows nginx (and all users) to read and write on this socket
chmod-socket = 666
# remove the socket when the process stops
vacuum = true
buffer-size = 524288
# loads your application one time per worker
# will very probably consume more memory,
# but will run in a more consistent and clean environment.
lazy-apps = true

uid = %(my_user)
gid = %(my_user)

# uWSGI will kill the process instead of reloading it
die-on-term = true
# socket file for getting stats about the workers
stats = %(my_app_folder)/stats.first_api.sock

# Scaling the server with the Cheaper subsystem

# set cheaper algorithm to use, if not set default will be used
cheaper-algo = spare
# minimum number of workers to keep at all times
cheaper = 5
# number of workers to spawn at startup
cheaper-initial = 5
# maximum number of workers that can be spawned
workers = 50
# how many workers should be spawned at a time
cheaper-step = 3

```
When you are finished, save and close the file.

one more file for our batch_api_code_modified_2 uwsgi.ini:
```
nano updated_version/batch_api_code_modified_2/uwsgi.ini
```
copy the following code to updated_version/batch_api_code_modified_2/uwsgi.ini and also adjust the required paths
```
[uwsgi]
# placeholders that you have to change
my_app_folder = /home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified_2
my_user = pdi

chdir = %(my_app_folder)
socket = %(my_app_folder)/sec_api.sock
#chdir = %(my_app_folder)
file = wsgi.py
callable = app

# environment variables
env = CUDA_VISIBLE_DEVICES=-1
#env = PYTHONPATH=%(my_app_folder):$PYTHONPATH

master = true
processes = 5
# allows nginx (and all users) to read and write on this socket
chmod-socket = 666
# remove the socket when the process stops
vacuum = true
buffer-size = 524288
# loads your application one time per worker
# will very probably consume more memory,
# but will run in a more consistent and clean environment.
lazy-apps = true

uid = %(my_user)
gid = %(my_user)

# uWSGI will kill the process instead of reloading it
die-on-term = true
# socket file for getting stats about the workers
stats = %(my_app_folder)/stats.sec_api.sock

# Scaling the server with the Cheaper subsystem

# set cheaper algorithm to use, if not set default will be used
cheaper-algo = spare
# minimum number of workers to keep at all times
cheaper = 5
# number of workers to spawn at startup
cheaper-initial = 5
# maximum number of workers that can be spawned
workers = 50
# how many workers should be spawned at a time
cheaper-step = 3

```
one more file for our parallel_listing uwsgi.ini:
```
nano updated_version/parallel_listing/uwsgi.ini
```
copy the following code to updated_version/parallel_listing/uwsgi.ini and also adjust the required paths
```
[uwsgi]
# placeholders that you have to change
my_app_folder = /home/pdi/real_estate_classification_api/updated_version/parallel_listing
my_user = pdi

chdir = %(my_app_folder)
socket = %(my_app_folder)/main_api.sock
#chdir = %(my_app_folder)
file = main_script.py
callable = app

# environment variables
env = CUDA_VISIBLE_DEVICES=-1

master = true
processes = 4
# allows nginx (and all users) to read and write on this socket
chmod-socket = 666
# remove the socket when the process stops
vacuum = true
buffer-size = 524288

# loads your application one time per worker
# will very probably consume more memory,
# but will run in a more consistent and clean environment.
lazy-apps = true

uid = %(my_user)
gid = %(my_user)

# uWSGI will kill the process instead of reloading it
die-on-term = true
# socket file for getting stats about the workers
stats = %(my_app_folder)/stats.production_ml.sock

# Scaling the server with the Cheaper subsystem

# set cheaper algorithm to use, if not set default will be used
cheaper-algo = spare
# minimum number of workers to keep at all times
cheaper = 5
# number of workers to spawn at startup
cheaper-initial = 5
# maximum number of workers that can be spawned
workers = 20
# how many workers should be spawned at a time
cheaper-step = 5


```

## Step 5 — Creating a systemd Unit File
Next, let’s create the systemd service unit file. Creating a systemd unit file will allow Ubuntu’s init system to automatically start uWSGI and serve the Flask application whenever the server boots.

Create a unit file ending in .service within the /etc/systemd/system directory to begin:
```
sudo nano /etc/systemd/system/batch_api_code_modified.service
```
copy the following content in batch_api_code_modified.service file and also adjust the required paths
```
[Unit]
Description=uWSGI instance to serve batch_api_code_modified service

[Service]
User=pdi
Group=www-data
WorkingDirectory=/home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified/
Environment="PATH=/home/pdi/real_estate_classification_api/venv_server/bin"
ExecStart=/home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini /home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified/uwsgi.ini
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

Create another unit file ending in .service within the /etc/systemd/system directory to begin:
```
sudo nano /etc/systemd/system/batch_api_code_modified_2.service
```
copy the following content in batch_api_code_modified_2.service file and also adjust the required paths
```
Description=uWSGI instance to serve batch_api_code_modified_2 service

[Service]
User=pdi
Group=www-data
WorkingDirectory=/home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified_2/
Environment="PATH=/home/pdi/real_estate_classification_api/updated_version/venv_server/bin"
ExecStart=/home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini /home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified_2/uwsgi.ini
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
Create another unit file ending in .service within the /etc/systemd/system directory to begin:
```
sudo nano /etc/systemd/system/parallel_listing.service
```
copy the following content in parallel_listing.service file and also adjust the required paths
```
[Unit]
Description=uWSGI instance to serve parallel listing service

[Service]
User=pdi
Group=www-data
WorkingDirectory=/home/pdi/real_estate_classification_api/updated_version/parallel_listing/
Environment="PATH=/home/pdi/real_estate_classification_api/venv_server/bin"
ExecStart=/home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini /home/pdi/real_estate_classification_api/updated_version/parallel_listing/uwsgi.ini
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
With that, our systemd service file is complete. Save and close it now.

##### We can now start the uWSGI service we created and enable it so that it starts at boot:
```
sudo systemctl start batch_api_code_modified
sudo systemctl enable batch_api_code_modified
sudo systemctl start batch_api_code_modified_2
sudo systemctl enable batch_api_code_modified_2
sudo systemctl start parallel_listing
sudo systemctl enable parallel_listing
```

##### Let's check the status:
```
sudo systemctl status <myproject> ( batch_api_code_modified_2 | batch_api_code_modified | parallel_listing)
```
You should see output like this:
```
Output
 myproject.service - uWSGI instance to serve myproject
   Loaded: loaded (/etc/systemd/system/myproject.service; enabled; vendor preset: enabled)
   Active: active (running) since Fri 2019-07-13 14:28:39 UTC; 46s ago
 Main PID: 30360 (uwsgi)
    Tasks: 6 (limit: 1153)
   CGroup: /system.slice/myproject.service
           ├─30360 /home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini myproject.ini
           ├─30378 /home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini myproject.ini
           ├─30379 /home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini myproject.ini
           ├─30380 /home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini myproject.ini
           ├─30381 /home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini myproject.ini
           └─30382 /home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini myproject.ini
```

If you see any errors, be sure to resolve them before continuing with the tutorial.

## Step 6 — Configuring Nginx to Proxy Requests
Our uWSGI application server should now be up and running, waiting for requests on the socket file in the project directory. Let's configure Nginx to pass web requests to that socket using the uwsgi protocol.

Begin by creating a new server block configuration file in Nginx's sites-available directory. Let's call this app_nginx.conf:
```
sudo nano /etc/nginx/sites-available/app_nginx.conf
note: change the server_name according to your vm dns or static ip
```
copy the following configurations to app_nginx.conf and also adjust the required paths
```

server {
    listen      4031;
    server_name ps-image-ai-05.stage.ylopo;
    charset     utf-8;
    client_max_body_size 75M;
    client_body_timeout 18000s;
    location / {
	#proxy_pass http://ps-image-ai-05.stage.ylopo:4031;
        include uwsgi_params;
        uwsgi_pass unix:/home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified/first_api.sock;
        uwsgi_read_timeout 18000;
    }    
    error_log /home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified/logs/error.txt;   
}

server {
    listen      4033;
    server_name ps-image-ai-05.stage.ylopo;
    charset     utf-8;
    client_max_body_size 75M;
    client_body_timeout 18000s;
    location / {
	#proxy_pass http://ps-image-ai-05.stage.ylopo:4033;
        include uwsgi_params;
        uwsgi_pass unix:/home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified_2/sec_api.sock;
        uwsgi_read_timeout 18000;
    }    
    error_log /home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified_2/logs/error.txt; 
}

server {
    listen      4034;
    server_name ps-image-ai-05.stage.ylopo;
    charset     utf-8;
    client_max_body_size 75M;
    client_body_timeout 18000s;
    location / {
	#proxy_pass http://ps-image-ai-05.stage.ylopo:4034;
        include uwsgi_params;
        uwsgi_pass unix:/home/pdi/real_estate_classification_api/updated_version/parallel_listing/main_api.sock;
        uwsgi_read_timeout 18000;
    }
    error_log /home/pdi/real_estate_classification_api/updated_version/parallel_listing/logs/error.txt;  
}



```
Save and close the file when you're finished.
To enable the Nginx server block configuration you've just created, link the file to the sites-enabled directory:
```
sudo ln -s /etc/nginx/sites-available/app_nginx.conf /etc/nginx/sites-enabled
```
With the file in that directory, we can test for syntax errors by typing:
```
sudo nginx -t
```
If this returns without indicating any issues, restart the Nginx process to read the new configuration:
```
sudo systemctl restart nginx
```
Finally, let's adjust the firewall to allow access to the Nginx server:
```
sudo ufw allow 'Nginx Full'
```

now we will create one more session for our server monitor service this will use to monitor database
```
tmux new -s monitor
```

next we will activate our server environment in this tmux session (assuming we are in *real_estate_classification_api*  directory)
```
source venv_server/bin/activate
```

lets create our database by using the following command
```
python updated_version/parallel_listing/create_database.py 
```

we have created our database now we will run our server script
```
python  updated_version/parallel_listing/monitor.py
```
Now again, detach from the Tmux session and return to your normal shell using
```
Ctrl+b d
```

We will create one more session for our web UI service.
```
tmux new -s website
```
next we will activate our web environment in this tmux session (assuming we are in *real_estate_classification_api*  directory)
```
source venv_web/bin/activate
```
First we will edit our main.py file and need to update the **BASE_URL** to *BASE_URL = http://localhost:4034* as this is the nginx  endpoint receiving clients requests.
```
nano website/main.py
```
Now, we will run our web script
```
python  website/main.py
```
Now again, detach from the Tmux session and return to your normal shell using
```
Ctrl+b d
```

**Finally**, we are done with our classification API and server setup.
##### [Restart Guide](https://github.com/Ali-Tahir/real_estate_classification_api/blob/master/docs/restart_guide.pdf)

## Api Endpoint Request Format
##### Updated version : [Request Guide](https://github.com/Ali-Tahir/real_estate_classification_api/blob/master/docs/request_guide.md)
###### Old Version : [Request Guide](https://github.com/Ali-Tahir/real_estate_classification_api/blob/master/docs/user_guide_old.pdf)



## Built With
##### Frameworks/Libraries
* [Python](https://www.python.org/downloads/release/python-360/) - Python is an interpreted, high-level, general-purpose programming language  - [Licence](https://en.wikipedia.org/wiki/Python_Software_Foundation_License).
* [Flask](https://palletsprojects.com/p/flask/) - Flask is a micro web framework  - [Licence](https://en.wikipedia.org/wiki/BSD_licenses).
* [Tensorflow](https://www.tensorflow.org/) - open source platform for machine learning - [License](https://en.wikipedia.org/wiki/Apache_License_2.0).
* [Pytorch](https://github.com/pytorch/pytorch) - open source machine learning library - [License](https://en.wikipedia.org/wiki/BSD_licenses).
* [Keras](https://keras.io/) - open source machine learning library - [License](https://en.wikipedia.org/wiki/MIT_License).

We have used all the free and open-source versions of libraries to create this project.

##### Models
* Keras Sequential Model - [License](https://en.wikipedia.org/wiki/MIT_License)
* Pytorch Pre-Trained Model - [License](https://github.com/kywch/Vis_places365/blob/master/LICENSE)
* Tensorflow Pre-Trained Model - [License](https://github.com/tensorflow/models/blob/master/LICENSE)

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/Ali-Tahir/real_estate_classification_api/tags). 

## Authors

* **Ali Tahir** - *Initial work* - [AliTahir](https://github.com/Ali-Tahir)
* **Javeria Ejaz** - *Initial work*
* **Sayad Afaq Ahmed** - *Initial work*

See also the list of [contributors](https://github.com/Ali-Tahir) who participated in this project.

## License

This project is licensed under the --- License

## Acknowledgments

* Hat tip to anyone whose code was used
