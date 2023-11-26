# Node Hello World

Simple node.js app that servers "A Monk in Cloud"

Great for testing simple deployments on Cloud

## Step 1: Install NodeJS and NPM using nvm
Install node version manager (nvm) by typing the following at the command line.

```bash
sudo su -
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```
Activate nvm by typing the following at the command line.

```bash
. ~/.nvm/nvm.sh
```

Use nvm to install the latest version of Node.js by typing the following at the command line.

```bash
nvm install node
```

Test that node and npm are installed and running correctly by typing the following at the terminal:

```bash
node -v
npm -v
```

## Step 2: Install Git and clone repository from GitHub
To install git, run below commands in the terminal window:

```bash
sudo apt-get update -y
sudo apt-get install git -y
```

Just to verify if system has git installed or not, please run below command in terminal:
```bash
git — version
```

This command will print the git version in the terminal.

Run below command to clone the code repository from Github:

```bash
git clone https://github.com/yeshwanthlm/nodejs-on-ec2.git
```

Get inside the directory and Install Packages

```bash
cd nodejs-on-ec2
npm install
```

Start the application
To start the application, run the below command in the terminal:

```bash
npm start
```

# This Script is to Install NodeJS & NPM on Ubuntu 22.04 in case if above installation doesn't work
#!/bin/bash

sudo apt-get update

sudo apt-get install -y ca-certificates curl gnupg

sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg

NODE_MAJOR=20

echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list

sudo apt-get update

## 2>/dev/null is given because it will give warning UI popup of Linux to skip that 
sudo apt-get install nodejs -y 2>/dev/null

sudo apt install npm -y

sudo npm install pm2 -g

============================================================

# To start the Nodejs application 

npm install

pm2 start index.js

============================================================

C-name in Nginx (Redirection to another dns)

Create a file in sudo vim /etc/nginx/sites-enabled/myapp


server {
    listen 800;
    server_name http://localhost;
    location /hello {
      return 301 https://google.com;
    }
    location /xyz {
      return 301 https://facebook.com;

    }
}

==============================================================

If you want to Run Nodejs app in nginx server (Connect Nodejs with Nginx server)

Set port 3000 in index.js file in Nodejs source code


Goto Nginx & create a file my-node-app in Sites-enabled dir # sudo vim /etc/nginx/sites-enabled/my-node-app

server {
    listen 8000;
    server_name http://15.206.189.193:3000/;	Replace the ServerIp in which nodejs is running & port number you have given in index.js

    location / {
        proxy_pass http://localhost:3000; # Change the port if your Node.js app runs on a different port
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }

}

========================================================

# If you want to redirect to google same above Node js app

server {
    listen 8000;
    server_name http://15.206.189.193:3000/;

    location / {
        proxy_pass http://localhost:3000; # Change the port if your Node.js app runs on a different port
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
    location /hello {
      return 301 https://google.com;
    }
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }

}

============================================


