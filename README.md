# nfs-persistentvolumes
Notes about setting up a Network File System in K8s

## Background story
Airflow (link) has support for KubernetesExecutor that allows running a task on a separate pod. Newly spawned pods need to read / write to a common shared volumn: reading DAGs and writing logs. This is solved by having a NFS, a shared volume between pods.

## Architecture

## Steps
- Creating a Persistent Disk in GCE

```
gcloud compute disks create --size=500GB --zone=europe-west1-b airflow-data-disk
```
- Creating NFS Server
```

```
