# Zabbix

This repo contains Zabbix Helm chart for deploying on Kubernetes.

## Installation

Nodes where Zabbix needs to be deployed must be labeled. There are three labels namely: `zabbix-mysql`, `zabbix-server` and `zabbix-web`. To label nodes use:

    $ kubectl label nodes node-list zabbix-mysql=true zabbix-server=true zabbix-web=true

Where:

 - `node-list` are nodes to label

To disable node selector just set `nodeselector` for server, mysql and web in `values.yaml` to `false`.  
Before installation fill `values.yaml` and to install Helm chart run:

    $ helm install some-chart-name --namespace=some-namespace-name --create-namespace path-to-chart-directory

Where:

- `some-chart-name` is Helm chart name
- `some-namespace-name` is optional argument that defines Kubernetes and Helm namespace where chart will be installed
- `path-to-chart-directory` is chart directory

## Values

Possible values to configure inside `values.yaml` are: 

 - `image` - defines image name
 - `imageTag` - defines image tag
 - `serviceName` - defines Kubernetes service name for component
 - `database` - defines Zabbix database name
 - `username` - defines MySQL user to login to database
 - `password` - defines MySQL password for user to login to database
 - `nodeSelector` - defines node selector usage (boolean) and possible values are `true` and `false`
 - `nodePort` - defines service port where service can be accessed outside cluster

`Storage section` enables using costum volume mounts. To use it set `subsection enabled` to `true` and fill `volumeMounts` and `volumes` fields according to Kubernetes documentation.

## Uninstallation

To full uninstall run:

    $ helm del some-chart-name -n some-namespace-name

Where:

- `some-chart-name` is Helm chart name for uninstall.
- `some-namespace-name` is optional argument that defines Helm namespace where chart is installed

## NOTES

Default password and username to login into Zabbix web interface is `Admin/zabbix`.
To save data mount `mysql` componente directory `/var/lib/mysql` to some host path.