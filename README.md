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

You can also directly add the plugins on the connect node . I have shared a sample below

```
apiVersion: platform.confluent.io/v1beta1
kind: Connect
metadata:
  name: connect
  namespace: confluent
spec:
  replicas: 2
  image:
    application: confluentinc/cp-server-connect:7.6.0
    init: confluentinc/confluent-init-container:2.8.0
  build:
    type: onDemand
    onDemand:
      plugins:
        locationType: confluentHub
        confluentHub:
          - name: kafka-connect-azure-event-hubs
            owner: confluentinc
            version: 2.0.4
          - name: kafka-connect-datagen
            owner: confluentinc
            version: 0.6.4
```
