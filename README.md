# Docker-SimpleWebAppFlask

# Simple Web Application using Python Flask

## 1. Install Required Dependencies
```bash
docker run -it ubuntu bash # login inside the container 
apt-get update
apt-get install -y python3
python3 --version   # Check Python installation
apt-get install -y python3-pip
apt-get update && apt-get install -y curl
```

## 2. Install and Configure Web Server
```bash
apt-get install -y python3-flask
```

# 3. Create a folder /opt and an application file app.py inside container:
```bash
mkdir -p /opt
cd /opt
nano app.py
```

# Write the following code in app.py:
```bash
import os
from flask import Flask
app = Flask(__name__)

@app.route("/")
def main():
    return "Welcome!"

@app.route('/how are you')
def hello():
    return 'I am good, how about you?'

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)
```

# 4. Start a Web Server
```bash
cd opt
FLASK_APP=app.py flask run --host=0.0.0.0 --port=8080
```

# 5. Test URL Inside your container
```bash
  # open another terminal
  # check running container 
    docker ps 
  # login inside the correct running container
    docker exec -it <container id> bash
    cd opt  
curl http://127.0.0.1:8080/
curl "http://127.0.0.1:8080/how%20are%20you
```  

# Dockerize the Application
# Create a DockerFile
```bash
mkdir my-simple-web-app
cd my-simple-web-app
cat > Dockerfile

FROM ubuntu

RUN apt-get update
RUN apt-get install -y python3
RUN apt-get install -y python3-pip
RUN apt-get install -y python3-flask

COPY app.py /opt/app.py

ENTRYPOINT FLASK_APP=/opt/app.py flask run --host=0.0.0.0 --port=8080
```
# Create app.py
```bash
import os
from flask import Flask
app = Flask(__name__)

@app.route("/")
def main():
    return "Welcome!"

@app.route('/how are you')
def hello():
    return 'I am good, how about you?'

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)
```
# Build the docker image with image name with tag <yourName>/my-simple-web-app
```bash
docker build . -t <dockerHubUserName>/my-simple-web-app
```
# Push the image to docker hub
```bash
sudo apt-get install -y gnome-keyring libsecret-1-0
# on prompt on docker hub create a password and use that password to login
docker login -u <dockerUserName>
docker push <imageName>
```

# Run the container with port mapping

