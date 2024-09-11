# Node Exporter Installation

I am using linux ubuntu machine for this installation. I spin up linux ubuntu machine in AWS cloud, and it is up and running.
I have also connected EC2 instance using iterm terminal in my Mac machine.

**Step 1**

Go to the website "https://prometheus.io/download/#node_exporter" and find the latest version of node exporter tar file.
Copy the link for that tar file.

![obs_28](../assets/obs_28.png)

**Step 2**

Run the command "wget <copied link>" in the terminal to download the tar file.

`wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz`

![obs_29](../assets/obs_29.png)

**Step 3**

Untar the downloaded file using the command "tar -xvzf <filename>.

`tar -xvzf node_exporter-1.8.2.linux-amd64.tar.gz`

![obs_30](../assets/obs_30.png)

**Step 4**

Navigate to node exporter directory (unzipped one)

![obs_31](../assets/obs_31.png)

**Step 5**

Start the node exporter executable file

![obs_32](../assets/obs_32.png)

**Step 6**

Open the browser and enter node exporter server IP followed by port number 9100.

![obs_33](../assets/obs_33.png)

***
Node exporter is up and running now.
However, if I close the terminal where node exporter executable is running or my EC2 instance is down,
then the node exporter also stops. Hence, this is not the ideal way to run the node exporter. 
The ideal way of running node exporter is to install and run as a service (systemd).
***

**The ideal way of running node exporter as a service.** 

**Step 1 - Create a system user for node exporter**

System username is `node_exporter`.
Before doing it, we need to ensure `node_exporter` user is not created yet. 

To do so, run the command `cat /etc/passwd | grep -i node_exporter`
If it returns value, it means `node_exporter` user is already available in the system.

We can create system user now. To create the user, run the below commands

```html
sudo useradd --no-create-home --shell /bin/false node_exporter
```

![obs_35](../assets/obs_35.png)

To check if the user is created successfully, run the command 

```html
cat /etc/passwd | grep -i node_exporter
```

![obs_36](../assets/obs_36.png)


**Step 2 - Copy the executable file to bin location**

To copy the node exporter to bin location, run the below commands

```html
sudo cp node_exporter /usr/local/bin/
```

![obs_34](../assets/obs_34.png)

**Step 3 - Assign permission and ownership to the system user**

To assign the ownership to `node exporter` user, run the below commands

```html
sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter
```

![obs_37](../assets/obs_37.png)

**Step 4 - Create a service file for node exporter**

Update the below content in the node exporter service file located at `/etc/systemd/system/node_exporter.service`

```html
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
```

![obs_38](../assets/obs_38.png)

**Step 5 - Reload the daemon service**

To do so, run the below command 

```html
systemctl daemon-reload
```

![obs_39](../assets/obs_39.png)

**Step 6 - Start the node exporter service**

To do so, run the below command 

```html
systemctl start node_exporter.service
```
![obs_40](../assets/obs_40.png)


**Step 7 - Check the status of the node exporter service**

To do so, run the below command 

```html
systemctl status node_exporter.service
```
![obs_41](../assets/obs_41.png)

**Step 8 - Enable the node exporter service**

To do so, run the below command.
This will ensure that the node exporter service automatically starts at system booting. 

```html
systemctl enable node_exporter.service
```
![obs_42](../assets/obs_42.png)

**Step 9 - Check the metrics are populated**

To do so, run the below command 

```html
curl localhost:9100/metrics
```
![obs_43](../assets/obs_43.png)

