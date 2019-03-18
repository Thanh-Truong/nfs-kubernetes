# nfs-persistentvolumes
Notes about setting up a Network File System in K8s

## Background story
[Airflow] (https://github.com/apache/airflow) has support for KubernetesExecutor that allows running a task on a separate pod. Newly spawned pods need to read / write to a common shared volumn: reading DAGs and writing logs. This is solved by having a NFS, a shared volume between pods.

## Architecture

## Steps
- Creating a Persistent Disk in GCE

```
gcloud compute disks create --size=500GB --zone=europe-west1-b airflow-logs-disk
gcloud compute disks create --size=500GB --zone=europe-west1-b airflow-dags-disk

```

- Creating NFS Server
```
kubectl apply -f nfs-server.yaml
```
After NSF Server deployment is up and running, its only container `nfs-server`
is accessible via the following service.

- Creating NFS Service to allow acessing to mounted volumn

```
kubectl apply -f nfs-server.yaml
```

- Creating NFS Persisent Volumn Claim, which maps to NFS Service
```
 kubectl apply -f nfs-pvc.yaml
```

## References:
- https://medium.com/platformer-blog/nfs-persistent-volumes-with-kubernetes-a-case-study-ce1ed6e2c266
- https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/
