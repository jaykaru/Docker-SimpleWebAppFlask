# Docker-SimpleWebAppFlask

# Simple Web Application using Python Flask

## 1. Install Required Dependencies
```bash
apt-get update
apt-get install -y python3
python3 --version   # Check Python installation
apt-get install -y python3-pip

## 2. Install and Configure Web Server
apt-get install -y python3-flask

# 3. Create a folder /opt and an application file app.py inside it:


mkdir -p /opt
cd /opt
nano app.py

# Write the following code in app.py:

from flask import Flask
app = Flask(__name__)

@app.route("/")
def home():
    return "Welcome!"

@app.route("/how are you")
def hello():
    return "I am good, how about you?"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)

# 4. Start a Web Server
FLASK_APP=app.py flask run --host=0.0.0.0 --port=8080

# 5. Test URL Inside your container

curl http://127.0.0.1:8080/
curl "http://127.0.0.1:8080/how are you"    


