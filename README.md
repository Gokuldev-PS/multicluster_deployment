# multicluster_deployment
This repo contains K8 configuration file to setup multiple kafka clusters using common control center .Both the kafka brokers share a common zookeeper

## Setup

1. If you need to add any connector use confluent hub CLI to install those which is installed on the connect nodes .Here is a sample command to how to open connect node bash

```
kubectl exec -it connect-0  -n confluent bash
}
```


2. Install the connector plugin using confluent hub CLI

https://www.confluent.io/hub/

```
confluent-hub install connectorname:version

```
