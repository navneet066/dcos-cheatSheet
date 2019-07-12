#### Command for getting the configured Cluster from CLI

```
dcos cluster list
```

#### Verify Login Credentials
```
dcos auth login
```

#### Verify services running on the cluster
```
dcos service
```

#### Checking status of the connected nodes
```
dcos node list
```

#### Retrieve detailed information about the current master node leader
```
dcos node log --leader
```
#### Retrieve detailed information about a specific node
```
dcos node log --mesos-id <nodeID>
```

#### Search for the package from the DCOS catalog
```
dcos package search redis
```
#### Install the package using the below commnd
```
dcos package install <PackageName> --yes 
```
#### Check the Status of a task from below command
```
dcos task
```
#### Review information for all deployed Marathon apps by running the following command
```
dcos marathon app list
```
#### Check the logs of a task
```
dcos task log <taskName>
```
#### You can also use dcos task to look up the Mesos ID for the any service, then open a secure shell using a command similar to the following:
```
dcos node ssh --master-proxy --mesos-id=dedbb786-feb7-47f2-ae69-27bf86ba53fb-S0
```
#### Deploy the sample app
```
dcos marathon app add https://raw.githubusercontent.com/joerg84/dcos-101/master/app1/app1.json
```
#### Create a single command service

single-cmd-app-cli.json
```
{
  "id": "/single-cmd-app-cli",
  "cmd": "sleep 10",
  "instances": 1,
  "cpus": 1,
  "mem": 128,
  "portDefinitions": [
    {
      "protocol": "tcp",
      "port": 10000
    }
  ],
  "requirePorts": false
}
```

after creating the json, Run the below command to create app:
```
dcos marathon app add single-cmd-app-cli.json
```

#### Create a simple containerized service
Create a json container-app-cli.json

```
{
  "id": "/container-hello-dcos-cli",
  "instances": 1,
  "cpus": 1,
  "mem": 128,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mesosphere/hello-dcos:<image-tag>",
      "forcePullImage": false,
      "privileged": false
    }
  },
  "acceptedResourceRoles": ["slave_public"],
  "portDefinitions": [
    {
      "protocol": "tcp",
      "port": 10001
    }
  ],
  "requirePorts": false
}

```

Start the service by running the following command:

```
dcos marathon app add container-app-cli.json

```
