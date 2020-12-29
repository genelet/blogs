# How to install LiuAlgoTrader?

LiuAlgoTrader is a scalable, multi-process framework for effective algorithmic trading. 
If you are planning to set up a ML trading system in Python, it is a good framework.
Find the home page of LiuAlgoTrader [here](https://github.com/amor71/LiuAlgoTrader). The author is
[amor71](mailto:amichay@sgeltd.com).

I installed it in a fresh Ubuntu 20.04 Desktop machine. Here is how-to.

<br />
<br />

## Chapter 1. Install Docker Engine and Docker Compose

Please follow up [the office document](https://docs.docker.com/engine/install/ubuntu/) to install Docker.

<br />

### 1.1) Remove Old Packages

```bash
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

You should get an error reporting that Docker is not found.

<br />

### 1.2) Add the Docker Repository

#### Preparing

```bash
$ sudo apt-get update
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

#### Verify the Signature

```bash
$ sudo apt-key fingerprint 0EBFCD88
```

#### Add the Repository

```bash
$ sudo add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"
```

<br />

### 1.3) Install the Docker Engine

```bash
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

#### Test 
```bash
$ sudo docker run hello-world
```

 You will get a report that the docker daemon is up and running correctly.
 The server will automatically be launched when the machine reboot.
 
 <br />
 
### 1.4) Normal User to Run Docker

Add user to the group:

```bash
$ sudo usermod -aG docker $USER
``` 

Run the same *hello-world* command without sudo:

```bash
$ newgrp docker
$ docker run hello-world
```

<br />

## Chapter 2. Install Docker Compose
 
Please follow up the [office document](https://docs.docker.com/compose/install/) to install Compose.
```bash
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

### 2.1) Test the installation.
```bash
$ docker-compose --version
docker-compose version 1.27.4, build 1110ad01
```

<br />
<br />

## Chapter 3. Install Python Tools
 
Python3 has already been installed in Ubuntu. Yet, you should install *pip* and *venv* to make a user-owned development environment
 separated from the machine-wide python.
 
Please see [this document](https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-programming-environment-on-an-ubuntu-20-04-server) for a complete installation guide.

<br />

### 3.1) Install *pip*

```bash
$ sudo apt install python3-pip build-essential libssl-dev libffi-dev python3-dev
```

<br />

### 3.2) Install *venv*

```bash
$ sudo apt install python3-venv
```

<br />

### 3.3) Setup New Environment
 
To create a new Python programming environment named *liu_env* and put the definition files in *pythons*, do:

```bash
$ mkdir pythons
$ cd pythons
$ python3 -m venv testing_env
```

A new directory called *liu_env* will be created under *pythons* which contains your environment directories and filess:
```bash
$ ls liu_env
bin include lib lib64 pyvenv.cfg share
```

<br />

### 3.4) Activate the Environment

```bash
$ source ./liu_env/bin/activate
(liu_env) you@machine:~/pythons
```
Your command prompt will now be prefixed with _(liu_env)_.

To deactivate
```bash
$ deactivate
you@machine:~/pythons
```

<br />

### 3.5) Create a *hello worl* Program

```bash
(liu_env) you@machine:~/pythons $ vi hello.py
```

and put this line into the new file

```lang-python
print("Hello, World!")
```

save and quit. And run
```bash
(liu_env) you@machine:~/pythons $ python hello.py
Hello, World!
```

<br />
<br />

## Chapter 4. Registration at Alpaca

Go to https://alpaca.markets to register an trading account. You need only the free paper trading account.

After login, go to _Paper Account_. On the right-hand side, find _Your API Keys_. _View_ it. 
You should _Regenerate Key_ for the 1st-time usage. 

Note that if you regenerate key, both the API Key ID and API Key Secret will be changed.

Save the ID and Secret in your environment:
```bash
$ export APCA_API_BASE_URL=https://paper-api.alpaca.markets
$ export APCA_API_KEY_ID=your_id
$ export APCA_API_SECRET_KEY=your_secret
```

<br />
<br />

## Chapter 5. Install LiuAlgoTrader

Make sure you are always under environment _(liu_env)_. Now you can use *python* and *pip* instead of *python3* and *pip3*.

<br />

### 5.1) Install *wheel*

You must install this package which is missing in LiuAlgoTrader.

```bash
$ pip install wheel
```
Note you don't use *pip3* but just *pip*.

<br />
 
### 5.2) Install the Main Package

```bash
$ pip install liualgotrader
```

It takes a while to finish, and then OK.

<br />

### 5.3) Configure the Framework

Run the command to go through the wizard, which will walk you through the configuration of environment variables, setup of a local dockerized PostgreSQL and pre-populate with test data.

```bash
$ liu quickstart
```

Follow the wizard instructions on screen. Answer "Yes" to all prompts.

<br />

### 5.4) Trade Simulation

Please follow the description on screen closely. This program will download and install Postgres SQL and simulate a daily paper trading. At the end of the quickstart, you will get a web page reporting the process and revenue.

You are now ready to build up your own stragery and trade!
