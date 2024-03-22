[!\[\](https://media-exp1.licdn.com/dms/image/C560BAQHk3Y2LoS1dgQ/company-logo_200_200/0?e=2159024400&v=beta&t=UoECQAIKrwna7isp_tJBzhK0CWSH2K3H4UepDDvgQOg)
# \[Kavtech\](http://www.kavtech.net/) - Real Estate Classification Api

Image classification technology has immense significance in real estate websites. Knowing the type of room in an image can help improve the end-user experience. However, manual tagging requires laborious work. Our image classification API automates the process by detecting the objects in the image and category of the image.
The Classification API has predictable resource-oriented URLs, accepts form-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.

## Getting Started

These instructions will get you a copy of the project up and running on your prod machine in no time.

### Prerequisites

What things you need before starting with installation.



* PLATFORM
```
Ubuntu, Windows
```

* HARDWARE
```
RAM 14-16GB, HARD DISK 40-60 GB, GPU MEM 4-15GB
```

* SOFTWARE
```
Nvidia Driver
CUDA 9.0 / 10.0 from Archive
Cudnn
mysql 5.5
```
* Update max_connections value to 500 in MySQL. Login to your MySQL terminal with the privileged user and execute the following query.
``` 
mysql> SET GLOBAL max_connections = 500;
```
* Set Cuda library path
```
ls /usr/local/ (this will list the directory, check the cuda version and use that version in below command)
sudo ldconfig /usr/local/cuda-10.0/lib64
```
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

you can check what we are going to achieve \[here\](https://github.com/Ali-Tahir/real_estate_classification_api/blob/master/docs/mechanism.pdf)
First we need to install git on our local machine
```
apt-get install git-core
```

Now, we should be able to run the following command to check our installed git version!

```
git --version
```

Clone the repository!

```
git clone git@github.com:Ali-Tahir/real_estate_classification_api.git
```

Move to your cloned repo directory using following command!

```
cd real_estate_classification_api
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
	cd ..
	```

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
\[uwsgi\]
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
\[uwsgi\]
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
\[uwsgi\]
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
\[Unit\]
Description=uWSGI instance to serve batch_api_code_modified service

\[Service\]
User=pdi
Group=www-data
WorkingDirectory=/home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified/
Environment="PATH=/home/pdi/real_estate_classification_api/venv_server/bin"
ExecStart=/home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini /home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified/uwsgi.ini
Restart=on-failure

\[Install\]
WantedBy=multi-user.target
```

Create another unit file ending in .service within the /etc/systemd/system directory to begin:
```
sudo nano /etc/systemd/system/batch_api_code_modified_2.service
```
copy the following content in batch_api_code_modified_2.service file and also adjust the required paths
```
Description=uWSGI instance to serve batch_api_code_modified_2 service

\[Service\]
User=pdi
Group=www-data
WorkingDirectory=/home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified_2/
Environment="PATH=/home/pdi/real_estate_classification_api/updated_version/venv_server/bin"
ExecStart=/home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini /home/pdi/real_estate_classification_api/updated_version/batch_api_code_modified_2/uwsgi.ini
Restart=on-failure

\[Install\]
WantedBy=multi-user.target
```
Create another unit file ending in .service within the /etc/systemd/system directory to begin:
```
sudo nano /etc/systemd/system/parallel_listing.service
```
copy the following content in parallel_listing.service file and also adjust the required paths
```
\[Unit\]
Description=uWSGI instance to serve parallel listing service

\[Service\]
User=pdi
Group=www-data
WorkingDirectory=/home/pdi/real_estate_classification_api/updated_version/parallel_listing/
Environment="PATH=/home/pdi/real_estate_classification_api/venv_server/bin"
ExecStart=/home/pdi/real_estate_classification_api/venv_server/bin/uwsgi --ini /home/pdi/real_estate_classification_api/updated_version/parallel_listing/uwsgi.ini
Restart=on-failure

\[Install\]
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
##### \[Restart Guide\](https://github.com/Ali-Tahir/real_estate_classification_api/blob/master/docs/restart_guide.pdf)

## Api Endpoint Request Format
##### Updated version : \[Request Guide\](https://github.com/Ali-Tahir/real_estate_classification_api/blob/master/docs/request_guide.md)
###### Old Version : \[Request Guide\](https://github.com/Ali-Tahir/real_estate_classification_api/blob/master/docs/user_guide_old.pdf)



## Built With
##### Frameworks/Libraries
* \[Python\](https://www.python.org/downloads/release/python-360/) - Python is an interpreted, high-level, general-purpose programming language  - \[Licence\](https://en.wikipedia.org/wiki/Python_Software_Foundation_License).
* \[Flask\](https://palletsprojects.com/p/flask/) - Flask is a micro web framework  - \[Licence\](https://en.wikipedia.org/wiki/BSD_licenses).
* \[Tensorflow\](https://www.tensorflow.org/) - open source platform for machine learning - \[License\](https://en.wikipedia.org/wiki/Apache_License_2.0).
* \[Pytorch\](https://github.com/pytorch/pytorch) - open source machine learning library - \[License\](https://en.wikipedia.org/wiki/BSD_licenses).
* \[Keras\](https://keras.io/) - open source machine learning library - \[License\](https://en.wikipedia.org/wiki/MIT_License).

We have used all the free and open-source versions of libraries to create this project.

##### Models
* Keras Sequential Model - \[License\](https://en.wikipedia.org/wiki/MIT_License)
* Pytorch Pre-Trained Model - \[License\](https://github.com/kywch/Vis_places365/blob/master/LICENSE)
* Tensorflow Pre-Trained Model - \[License\](https://github.com/tensorflow/models/blob/master/LICENSE)

## Versioning

We use \[SemVer\](http://semver.org/) for versioning. For the versions available, see the \[tags on this repository\](https://github.com/Ali-Tahir/real_estate_classification_api/tags). 

## Authors

* **Ali Tahir** - *Initial work* - \[AliTahir\](https://github.com/Ali-Tahir)
* **Javeria Ejaz** - *Initial work*
* **Sayad Afaq Ahmed** - *Initial work*

See also the list of \[contributors\](https://github.com/Ali-Tahir) who participated in this project.

## License

This project is licensed under the --- License

## Acknowledgments

* Hat tip to anyone whose code was used
](README.md)