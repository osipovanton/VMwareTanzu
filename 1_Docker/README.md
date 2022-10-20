# Instal WSL
```powershell
wsl --unregister Ubuntu-20.04

wsl --list --onlin

wsl --install -d Ubuntu-20.04

wsl --list
```

![image](https://user-images.githubusercontent.com/79700810/196971403-0b6f821b-07d8-4896-8875-8e17e578f909.png)

# Install Docker
```
sudo -i
apt-get update
apt-get install -y ca-certificates curl gnupg lsb-release
```

![image](https://user-images.githubusercontent.com/79700810/196971710-b2e502cf-285a-42b1-8a83-ba462fe037aa.png)

```
mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

![image](https://user-images.githubusercontent.com/79700810/196971959-4b2a40e3-5803-4ada-91eb-62b4fe15e5d5.png)

```
service docker start
```

# Create folder

```
mkdir /home/user/docker
chmod -R 777 /home/user/docker/
```

## Dockerfile

hello.py

from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"



Dockerfile

# syntax=docker/dockerfile:1
FROM ubuntu:22.04

# install app dependencies
RUN apt-get update && apt-get install -y python3 python3-pip
RUN pip install flask==2.1.*

# install app
COPY hello.py /

# final configuration
ENV FLASK_APP=hello
EXPOSE 8000
CMD flask run --host 0.0.0.0 --port 8000


docker build -t hello:latest .


docker run --name hello -p 8000:8000 -d hello:latest










docker run docker.io/busybox:latest date



docker run -it busybox sh

ps

docker run --rm -d --name httpd -p 8080:80 busybox httpd -f -vv


###

docker ps -a
docker rm $(docker ps -aq)
###

docker build -t greeting .

docker history greeting


docker run --rm greeting

docker run --rm greeting /goodbye






docker rmi greeting
docker build -t greeting .
docker run -it --rm greeting /bin/bash
