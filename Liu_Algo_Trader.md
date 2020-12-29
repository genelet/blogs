# How to install LiuAlgoTrader?

LiuAlgoTrader is a scalable, multi-process framework for effective algorithmic trading. 
If you are planning to set up a ML trading system in Python, it is a good framework.

I installed it in a fresh Ubuntu 20.04 Desktop machine. Here is how-to.

## Install Docker Engine and Docker Composer

https://docs.docker.com/engine/install/ubuntu/

### Remove possible existing docker and associated packages

> $ sudo apt-get remove docker docker-engine docker.io containerd runc

You should get an error reporting that docker is not found.

### Add the Docker repository

Preparing:

> $ sudo apt-get update
>
> $ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
>
> $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Verifying that the download has the right siganiture:

> $ sudo apt-key fingerprint 0EBFCD88

Add the repository:

> $ sudo add-apt-repository \
>   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
>   $(lsb_release -cs) \
>   stable"
   
Install the Docker Engine:
  
> $ sudo apt-get update
>
> $ sudo apt-get install docker-ce docker-ce-cli containerd.io
 
Test the installation is correct
 
> $ sudo docker run hello-world
 
 You will get a report that the docker daemon is up and running correctly.
 The server will automatically be launched when the machine reboot.
 
### Let a normal user to run docker
 
 Add your user account to the docker group:
 
> $ sudo usermod -aG docker $USER
 
 Run the same hello-world docker command without sudo:

> $ newgrp docker
>
> $ docker run hello-world
 
 
## Install Docker Composer
 
 https://docs.docker.com/compose/install/
 
> $ sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
>
> $ sudo chmod +x /usr/local/bin/docker-compose
 
 Test the installation.

> $ docker-compose --version
>
> docker-compose version 1.27.4, build 1110ad01


## Install Python tools
 
 Python3 has already been installed in Ubuntu. Yet, you should install *pip* and *venv* to make a user-owned development environment
 separated from the machine-wide python environment.
 
 https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-programming-environment-on-an-ubuntu-20-04-server
 
### Install pip
 
> $ sudo apt install python3-pip build-essential libssl-dev libffi-dev python3-dev
 
### install venv
 
> $ sudo apt install -y python3-venv
 
### Set up a special python environment
 
Assuming you want to create a new Python programming environment and have the associatged definition files in "pythons", do:

> $ mkdir pythons
>
> $ cd pythons
 
Then create an environment by running the following command:

> $ python3 -m venv testing_env

A new directory called "liu_env" will be created under "pythons" which contains a few items defining your environments:

> $ ls liu_env
>
> bin include lib lib64 pyvenv.cfg share

### Activate the environment

> $ source ./liu_env/bin/activate

Your command prompt will now be prefixed with _(liu_env)_.

to deactivate

> $ deactivate

Note that under the _liu_env_, you should use *python* and *pip*, instead of *python3* and *pip3*.

### Create a hello worl program

> (liu_env) you@machine:~/pythons $ vi hello.py

and put this line in the new file

> print("Hello, World!")

save and quit. And run

> (liu_env) you@machine:~/pythons $ python hello.py

it should output

> Hello, World!


## Registration at Alpaca

Go to https://alpaca.markets to register an trading account. You need only the free paper trading account to
run this LiuAlgoTrader . 

After login, go to _Paper Account_. On the right-hand side, find _Your API Keys_. _View_ it. 
You should _Regenerate Key_ for the 1st-time usage. Note that if you regenerate key, both the API Key ID and API Key Secret will be changed.

Save the ID and Secret in your environment:
 
- $ export APCA_API_BASE_URL=https://paper-api.alpaca.markets
- $ export APCA_API_KEY_ID=your_id
- $ export APCA_API_SECRET_KEY=your_secret


## Install LiuAlgoTrader

Make sure you are under _(liu_env)_. 

### install "wheel"

You must install this package which is missing in the fresh Ubuntu

> $ pip install wheel
 
 (note we don't use *pip3* but just *pip*)
 
 
### install the main package

> $ pip install liualgotrader

it takes a while, and then OK

### Configure the framework

The wizard will walk you through the configuration of environment variables, setup of a local dockerized PostgreSQL and pre-populate with test data.

run

> $ liu quickstart

and follow the installation wizard instructions. Answer "Yes" to all promotes.


### Trade Simulation

Please follow the description on screen closely. This program will download and install Postgres SQL and simulate a daily paper trading. At the end of the quickstart, you will get a web page reporting the process and revenue.
