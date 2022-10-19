# psql-client

This repo build a docker image base on alpine that runs a psql client.

## Connect to a PostgreSQL database

``` bash
docker run --rm -it --name postgresql-client andreswebs/postgresql-client -h <host_ip_address> -p <port> -U <user> -W
```

To get a shell inside the running container:

```
docker exec -it postgresql-client /bin/sh
```

## Running on kubernetes

### Prerequisites

You need a working k8s cluster and `kubectl` configured.

### Deploy the objects:

In [k8s/pod.yaml](./k8s/pod.yaml), you can find the manifest to run a pod.


Use below command to deploy the pod
``` bash
# deploy pod
kubectl apply -f pod.yml

# get a shell of the 
kubectl exec -it postgresql-client -- /bin/sh

# general form
psql -h <host_ip_address> -p <port> -U <user> -W

# connect to a postgresql svc (via service ip)
psql -h 10.233.36.23 -U keycloak -W

# via k8s service fqdn
psql -h keycloak-postgres-postgresql.keycloak.svc.cluster.local -U keycloak -W
```