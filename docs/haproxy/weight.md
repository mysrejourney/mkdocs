# Weighted Round-Robin Algorithm

It distributes the requests to the servers based on the weightage defined. It doesn't consider the server capacity or load.

![ha_13.png](../assets/ha_13.png)

Let us assume that there are three servers running in the cluster,
and the incoming requests are distributed among these three servers
and the scheduling algorithm is configured as `weighted round-robin` algorithm.
The weightages of the servers are 2,1,3 respectively (Higher number is the higher priority).

If there are six incoming requests to the load balancer,
three of the incoming requests go to the third server,
two of the incoming requests go to the first server, and one request goes to the second server.


## HA Proxy configuration for weighted round-robin

I am running HA proxy in EC2 ubuntu machine.
I am also creating three APIs running on different ports using Flask application.
I created docker images for these three APIs and created docker image for HA proxy configuration as well.
I am running everything in docker compose file.

**HAproxy.cfg**

```html
global
    log stdout format raw local0
    daemon

defaults
    log     global
    mode    http
    option  httplog
    option  dontlognull
    timeout connect 5000ms
    timeout client  50000ms
    timeout server  50000ms

frontend http_front
    bind *:8888
    default_backend servers

backend servers
    balance roundrobin
    server server1 app1:5001 weight 2 check
    server server2 app2:5002 weight 1 check
    server server3 app3:5003 weight 3 check

```

![ha_14.png](../assets/ha_14.png)

**app1.py**

```html
from flask import Flask, request

app = Flask(__name__)

@app.route('/', methods=['GET'])
def home():
    return "Hello from Flask from app 1!"

@app.route("/data")
def data():
    return "Data from Flask app 1!"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)

```

**app2.py**

```html
from flask import Flask, request

app = Flask(__name__)

@app.route('/', methods=['GET'])
def home():
    return "Hello from Flask from app 2!"

@app.route("/data")
def data():
    return "Data from Flask app 2!"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5001)

```

**app3.py**

```html
from flask import Flask, request

app = Flask(__name__)

@app.route('/', methods=['GET'])
def home():
    return "Hello from Flask from app 3!"

@app.route("/data")
def data():
    return "Data from Flask app 3!"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5002)

```

**Dockerfile.app1**

```html
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY app1.py .

# Install any needed packages specified in requirements.txt
RUN pip install flask

# Make port 5000 available to the world outside this container
EXPOSE 5000

# Run app.py when the container launches
CMD ["python", "app1.py"]
```

**Dockerfile.app2**

```html
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY app2.py .

# Install any needed packages specified in requirements.txt
RUN pip install flask

# Make port 5001 available to the world outside this container
EXPOSE 5001

# Run app.py when the container launches
CMD ["python", "app2.py"]
```
**Dockerfile.app3**

```html
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY app3.py .

# Install any needed packages specified in requirements.txt
RUN pip install flask

# Make port 5002 available to the world outside this container
EXPOSE 5002

# Run app.py when the container launches
CMD ["python", "app3.py"]
```

**Dockerfile.haproxy**

```html
# Use the official HAProxy image from Docker Hub
FROM haproxy:latest

# Copy the custom HAProxy configuration file into the container
COPY haproxy.cfg /usr/local/etc/haproxy/haproxy.cfg

# Expose the port for HAProxy
EXPOSE 8888
```

**docker-compose.yml**

```html
version: '3'

services:
  app1:
    build:
      context: .
      dockerfile: Dockerfile.app1
    container_name: flask_app1
    ports:
      - "5000:5000"

  app2:
    build:
      context: .
      dockerfile: Dockerfile.app2
    container_name: flask_app2
    ports:
      - "5001:5001"

  app3:
    build:
      context: .
      dockerfile: Dockerfile.app3
    container_name: flask_app3
    ports:
      - "5002:5002"

  haproxy:
    build:
      context: .
      dockerfile: Dockerfile.haproxy
    container_name: haproxy
    ports:
      - "8888:8888"
    depends_on:
      - app1
      - app2
      - app3
```

Now, we have all the configurations are in place. 

![ha_6.png](../assets/ha_6.png)

Let us create the containers using `docker compose up -d` command

![ha_7.png](../assets/ha_7.png)

Hit the load balance url a couple of times. Each time the request goes to different server.

![ha_11.png](../assets/ha_11.png)

![ha_9.png](../assets/ha_9.png)

![ha_11.png](../assets/ha_11.png)

![ha_10.png](../assets/ha_10.png)

![ha_11.png](../assets/ha_11.png)

![ha_9.png](../assets/ha_9.png)

Check the logs of the ha proxy container

![ha_15.png](../assets/ha_15.png)

