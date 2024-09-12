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

## Integrate Node Exporter with Prometheus

Prometheus scrapes the target and pulls the metrics.
So, it should know what the target is prior to pull the metrics.
Prometheus target configuration is configured in the `prometheus.yml` file by default.
Hence, we need to update the configuration file with the target details of node exporter server details.
After this change, restart the prometheus.
Then, Prometheus will start to scrape the node metrics after restarting the prometheus.

**Step 1 - Check Prometheus server status and Node exporter status**

Connect the prometheus server in the terminal and run the following command.

```html
systemctl status prometheus.service
```
![obs_44](../assets/obs_44.png)

Connect the node exporter machine in the terminal and run the following command.

```html
systemctl status node_exporter.service
```

![obs_45](../assets/obs_45.png)

**Step 2 - Update prometheus configuration file**

Add the node server ip address in the target section to ensure prometheus knows what machine it needs to scrape.

```html
  - job_name: "Node server"
    scrape_interval: 10s
    scrape_timeout: 5s
    metrics_path: /metrics
    static_configs:
      - targets: ["172.31.84.187:9100"]
```

![obs_46](../assets/obs_46.png)

**Step 3 - Restart Prometheus Server**

Connect the prometheus server in the terminal and run the following command.

```html
systemctl restart prometheus.service
```
![obs_47](../assets/obs_47.png)

**Step 4 - Check Prometheus server status**

Connect the prometheus server in the terminal and run the following command.

```html
systemctl status prometheus.service
```
![obs_44](../assets/obs_44.png)

**Step 5 - Check Prometheus UI for target status**

Open the browser and enter the <prometheus server IP:9090>. 

![obs_48](../assets/obs_48.png)

Click on the menu "Status -> Targets"

![obs_49](../assets/obs_49.png)

As we see, prometheus server is able to understand the node service and where it is running,
what is the current state, etc. 

If we go to the "graph" menu, and type "node" you will be able to see all the metrics related to node service.

![obs_50](../assets/obs_50.png)

That's all. Simple, isn't it? 