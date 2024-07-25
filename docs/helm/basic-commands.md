# Basic Helm Commands

All the helm commands are executed in command line interface (helm cli).

### 1. helm help
This is the command that helps you find out the right command to do something.

![helm_2.png](../assets/helm_2.png)


### 2. helm search

There are two ways to search the chart.

2.1. Search in the artifacthub.io - ```helm search hub <chart name>```
![helm_13.png](../assets/helm_13.png)


2.2. Search in the repository - ```helm search repo <chart name>```
![helm_14.png](../assets/helm_14.png)


But before run `helm search repo <chart name>` command, you must ensure that the repo has been added in your machine.
To do so, run the command `helm repo add <repository url>`

![helm_15.png](../assets/helm_15.png)


### 3. helm install

Before installing any chart, you must need to ensure that the repository is added locally. To do so, 
run the command `helm repo add <repository url>`

![helm_15.png](../assets/helm_15.png)

To verify if the repo is added or not, use `helm repo list` command

![helm_16.png](../assets/helm_16.png)

Now, install the chart using `helm install <release name> <repo name>/<chart name>`

![helm_17.png](../assets/helm_17.png)

In the above snapshot, my-prometheus is the release name, prometheus-community is the repo name, and prometheus is the 
chart name. After installing the chart, validate the resources created in the k8s cluster.

![helm_18.png](../assets/helm_18.png)

To install a specific version, run the below command
`helm install <release name> <repo name>/<chart name> --version <version number>`

![helm_29.png](../assets/helm_29.png)

### 4. helm list
This is the command that helps you list all the releases in your k8s cluster.

![helm_19.png](../assets/helm_19.png)


### 5. helm uninstall
This is the command that helps you uninstall the releases in your k8s cluster.

![helm_20.png](../assets/helm_20.png)

After uninstalling the chart, validate the resources deleted in the k8s cluster.

![helm_21.png](../assets/helm_21.png)

## Sub Commands

You can find the sub commands using `helm <command> help`

![helm_22.png](../assets/helm_22.png)

### 6. helm repo list
This command lists all the repository added in your local machine.

![helm_23.png](../assets/helm_23.png)

### 7. helm repo remove
This command lists all the repository removed in your local machine.

![helm_24.png](../assets/helm_24.png)

`Remember that when you install any chart, default values will be picked and created k8s objects in the cluster.
You cannot modify that during the installation of the chart`

If you want to override the default values, there are three ways.

**First approach**

Overrides the values through runtime arguments like below

```html
helm install --set <variable name>=<value to override> <repo name>/<chart name>

Example:
helm install --set replicaCount=3 prometheus-community/prometheus

helm install --set replicaCount=3 --set maintainer="satheeshpandianj@gmail.com" prometheus-community/prometheus
```

**Second approach**

Keep all the values to be overridden in a separate YAML file and pass that file during installation.

```html
custom-file.yaml

replicaCount: 1
maintainer: "satheeshpandianj@gmail.com"
```

```html
helm install --values <YAML file name including the path> <repo name>/<chart name>

Example:
helm install --values ~/custom-file.yaml prometheus-community/prometheus

```
**Third approach**

Download the chart directory locally and update `values.yaml` file with updated values.
To do so, use the below command

`helm pull <repo name> or helm pull --untar <repo name>`

![helm_25.png](../assets/helm_25.png)

![helm_26.png](../assets/helm_26.png)

Then install the chart from locally. To do so, use the below command
`helm install <release name> <local repo directory path>`

![helm_27.png](../assets/helm_27.png)


### 8. helm history

This command helps to see all the revisions for a particular release.
`helm history <release name>`

![helm_28.png](../assets/helm_28.png)

### 9. helm rollback

This command helps to roll back to a previous version for a particular release.
`helm rollback <release name>`

![helm_28.png](../assets/helm_28.png)

