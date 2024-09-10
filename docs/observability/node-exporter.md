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
However, if I close the terminal where node exporter executable is running or my EC2 instance si down,
then the node exporter also stops. Hence, this is not the ideal way to run the node exporter. 
The ideal way of running node exporter is to install and run as a service (systemd).
***



