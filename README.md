# Slurm Docker Cluster

The compose file will create the following named volumes:

* etc_munge         ( -> /etc/munge     )
* etc_slurm         ( -> /etc/slurm     )
* slurm_jobdir      ( -> /data          )
* var_lib_mysql     ( -> /var/lib/mysql )
* var_log_slurm     ( -> /var/log/slurm )

## Building the Docker Image

Build the image locally:

```console
docker build -t docker-slurm .
```


> Note: You will need to update the container image version in
> [docker-compose.yml](docker-compose.yml).



## Starting the Cluster

Run `docker-compose` to instantiate the cluster:

```console
docker-compose up -d
```

## Register the Cluster with SlurmDBD


```console
./register_cluster.sh
```

>
> You can check the status of the cluster by viewing the logs: `docker-compose
> logs -f`

## Accessing the Cluster

Use `docker exec` to run a bash shell on the controller container:

```console
docker exec -it slurmctld bash
```

## Deleting the Cluster

To remove all containers and volumes, run:

```console
docker-compose stop
docker-compose rm -f
docker volume rm slurm-docker-cluster_etc_munge slurm-docker-cluster_etc_slurm slurm-docker-cluster_slurm_jobdir slurm-docker-cluster_var_lib_mysql slurm-docker-cluster_var_log_slurm
```
