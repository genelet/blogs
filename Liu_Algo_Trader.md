- How to install LiuAlgoTrader?

LiuAlgoTrader is a scalable, multi-process framework for effective algorithmic trading. 
If you are planning to set up a ML trading system in Python, it is a good starting point.

I installed it in a fresh Ubuntu 20.04 Desktop machine. Here is how-to.

-- Install Docker Engine and Docker Composer

https://docs.docker.com/engine/install/ubuntu/

--- Remove possible existing docker and associated packages

sudo apt-get remove docker docker-engine docker.io containerd runc

For a fresh Ubuntu, you should get an error reporting that docker is not found.

--- Use Docker repository

Preparing:

$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
    
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Verifying that the download has the right siganiture:

$ sudo apt-key fingerprint 0EBFCD88

Add the repository:

$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
   
  Install
  
  $ sudo apt-get update
 $ sudo apt-get install docker-ce docker-ce-cli containerd.io
 
 Test the installation is correct
 
 $ sudo docker run hello-world
 
 You will get a report that the docker daemon is up and running correctly.
 The server will automatically be launched when the machine reboot.
 
 --- Let a normal user to run docker
 
 Add your user account to the docker group:
 
 $ sudo usermod -aG docker $USER
 
 Run the same hello-world docker command without sudo:
 
 $ newgrp docker 
 
 $ docker run hello-world
 
 -- Install Docker Composer
 
 https://docs.docker.com/compose/install/
 
 sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 
 sudo chmod +x /usr/local/bin/docker-compose
 
 Test the installation.

$ docker-compose --version
docker-compose version 1.27.4, build 1110ad01


 -- Install Python tools
 
 Python3 has already been installed in Ubuntu. Yet, you should install *pip* and *venv* to make a user-owned development environment
 separated from the machine-wide python environment.
 
 https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-programming-environment-on-an-ubuntu-20-04-server
 
 --- Install pip
 
 sudo apt install python3-pip build-essential libssl-dev libffi-dev python3-dev
 
 --- install venv
 
 sudo apt install -y python3-venv
 
 --- Set up a special environment
 
Assuming you want to create a new Python programming environment and have the associatged definition files in "pythons", do:

mkdir pythons
cd pythons
 
Then create an environment by running the following command:

python3 -m venv testing_env

A new directory called "liu_env" will be created under "pythons" which contains a few items defining your environments:

ls liu_env
bin include lib lib64 pyvenv.cfg share

--- Activate this environment

source ./liu_env/bin/activate

Your command prompt will now be prefixed with (liu_env).

to deactivate

deactivate

Note that under your liu_env, you can and should use python and pip, instead of python3 and pip3.

--- Create a hello worl program

(liu_env) you@machine:~/pythons $ vi hello.py

and put this line in the new file
print("Hello, World!")

save and quit. And run

(liu_env) you@machine:~/pythons $ python hello.py

it should output

Hello, World!

-- Install LiuAlgoTrader

--- Register at Alpaca

Go to ... to register and get a paper trading account. This is free if you live in the US.

At the end, you will get 
Make sure you are under liu_env. 

--- install "wheel"

You must install this package which is missing in the fresh Ubuntu

 pip install wheel
 
 (note that in liu_env, you don't use pip3 but just pip)
 
 
--- install the main package

pip install liualgotrader

it takes a while, and then OK

--- Configure the framework

The wizard will walk you through the configuration of environment variables, setup of a local dockerized PostgreSQL and pre-populate with test data.

run

$ liu quickstart

and follow the installation wizard instructions. Answer "Yes" to all promotes. Note that at this 

 
 
