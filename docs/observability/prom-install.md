# Prometheus Installation

I am using linux ubuntu machine for this installation. I spin up linux ubuntu machine in AWS cloud, and it is up and running.
I have also connected EC2 instance using iterm terminal in my Mac machine.

**Step 1**

Go to the website "https://prometheus.io/download/" and find the latest version of prometheus tar file.
Copy the link for that tar file.

![obs_5](../assets/obs_5.png)

**Step 2**

Run the command "wget <copied link>" in the terminal to download the tar file.

`wget https://github.com/prometheus/prometheus/releases/download/v2.54.1/prometheus-2.54.1.linux-amd64.tar.gz`

![obs_6](../assets/obs_6.png)

**Step 3**

Untar the downloaded file using the command "tar -xvzf <filename>.

`tar -xvzf prometheus-2.54.1.linux-amd64.tar.gz`

![obs_7](../assets/obs_7.png)

**Step 4**

Navigate to prometheus directory (unzipped one)

![obs_8](../assets/obs_8.png)

**Step 5**

Start the prometheus executable file (This is nothing but prometheus server)

![obs_9](../assets/obs_9.png)

**Step 6**

Open the browser and enter prometheus server IP followed by port number 9090.

![obs_10](../assets/obs_10.png)

Stopping prometheus server

![obs_11](../assets/obs_11.png)

Now prometheus UI is not working.

![obs_12](../assets/obs_12.png)

***
Prometheus is up and running now.
However, if I close the terminal where prometheus executable is running or my EC2 instance is down, then the prometheus
also stops. Hence, this is not the ideal way to run the prometheus.
***


**The ideal way of running prometheus is to install and run as a service.** 

To do so, we need to follow below steps

**Step 1 - Update the system packages**

 Run the command 
```html 
sudo apt update
```

![obs_13](../assets/obs_13.png)

**Step 2 - Create a system user for prometheus**

System username is `prometheus`.
Before doing it, we need to ensure `prometheus` user is not created yet. 

To do so, run the command `cat /etc/passwd | grep -i prometheus`
If it returns value, it means `prometheus` user is already available in the system.

![obs_14](../assets/obs_14.png)

As the above command returns nothing, we can create system user now. To create the user, run the below commands

```html
sudo groupadd --system prometheus
sudo useradd -s /sbin/nologin --system -g prometheus prometheus
```
![obs_15](../assets/obs_15.png)


Let us ensure the user `prometheus` is created.

```html
cat /etc/passwd | grep -i prometheus
```

![obs_16](../assets/obs_16.png)


**Step 3 - Create Directories for Prometheus**

To store configuration files and libraries for Prometheus, you need to create a few directories. 
The directories will be located in the `/etc` and the `/var/lib` directory respectively. 
Use the commands below to create the directories:

```html
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
```

![obs_17](../assets/obs_17.png)

**Step 4 - Move the Binary Files & Set Owner**

Navigate to the prometheus directory. You need to move some binary files (prometheus and promtool) and change the 
ownership of the files to the "prometheus" user and group. You can do this with the following commands:

```html
sudo mv prometheus /usr/local/bin
sudo mv promtool /usr/local/bin

# set the owner 
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool
```

![obs_18](../assets/obs_18.png)


**Step 5 - Move the Configuration Files & Set Owner**

Next, move the configuration files and set their ownership so that Prometheus can access them. 
To do this, run the following commands:

```html
sudo mv consoles /etc/prometheus
sudo mv console_libraries /etc/prometheus
sudo mv prometheus.yml /etc/prometheus

# set the owner 
sudo chown prometheus:prometheus /etc/prometheus
sudo chown -R prometheus:prometheus /etc/prometheus/consoles
sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries
sudo chown -R prometheus:prometheus /var/lib/prometheus
```

![obs_19](../assets/obs_19.png)

The `prometheus.yml` file (/etc/prometheus/prometheus.yml) is the main Prometheus configuration file. 
It includes settings for targets to be monitored, data scraping frequency, data processing, and storage.


![obs_20](../assets/obs_20.png)


**Step 6 - Create Prometheus Systemd Service**

Now, you need to create a system service file for Prometheus. 
Create and open a prometheus.service file with the vi text editor using:

```html
vi /etc/systemd/system/prometheus.service
```
Content of the file is

```html
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
```

![obs_21](../assets/obs_21.png)

**Step 7 - Reload Systemd**

You need to reload the system configuration files after saving the prometheus.service file so that changes made 
are recognized by the system. Reload the system configuration files using the following:

```html
sudo systemctl daemon-reload
```

![obs_22](../assets/obs_22.png)

**Step 8 - Start Prometheus Service**

Next, you want to enable and start your Prometheus service. Do this using the following commands:

```html
sudo systemctl enable prometheus
sudo systemctl start prometheus
```

![obs_23](../assets/obs_23.png)


**Step 9 - Check Prometheus Status**

After starting the Prometheus service, you may confirm that it is running or if you have encountered errors using:

```html
sudo systemctl status prometheus
```

![obs_24](../assets/obs_24.png)

**Step 10 - Update firewall rules**
Prometheus runs on port 9090 by default, so you need to allow port 9090 on your firewall, Do that using the command:

```html
sudo ufw allow 9090/tcp
```

![obs_25](../assets/obs_25.png)

With Prometheus running successfully, you can access it via your web browser using <ip_address>:9090

![obs_26](../assets/obs_26.png)

Run the query in prometheus UI.

![obs_27](../assets/obs_27.png)