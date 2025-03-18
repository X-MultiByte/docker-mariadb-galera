# MariaDB Galera Cluster with Docker Compose

## Overview
This project provides a **MariaDB Galera Cluster** running in **Docker Compose**. 
It is designed for **High Availability, Automatic Failover, and Data Replication** across multiple database nodes.

## Features
✅ **Three-node MariaDB Galera Cluster** running inside Docker containers.
✅ **Automatic cluster synchronization** using `wsrep` replication.
✅ **Persistent storage using Docker volumes**, ensuring data is not lost when containers restart.
✅ **Network isolation**, using a dedicated `galera-cluster` network for secure communication.
✅ **Local machine simulation**, enabling easy testing and demonstration of database high availability.

## Prerequisites
Before you start, ensure you have:
- Docker & Docker Compose installed on your system
- At least **2 CPU cores & 4GB RAM** available (recommended for local testing)

## Getting Started
### 1️⃣ Clone this repository
```sh
git clone https://github.com/X-MultiByte/docker-mariadb-galera.git
cd docker-mariadb-galera
```

### 2️⃣ Start the Cluster
```sh
docker-compose up -d
```
This command will start three **MariaDB Galera** nodes as Docker containers.

### 3️⃣ Verify Cluster Status
Check if all three nodes have successfully joined the cluster:
```sh
docker exec -it mariadb-node1 mysql -uroot -prootpassword -e "SHOW STATUS LIKE 'wsrep_cluster_size';"
```
If the output is `3`, your cluster is running successfully! 🎉

### 4️⃣ Connect to the Database
To connect to any node, use:
```sh
docker exec -it mariadb-node1 mysql -uroot -prootpassword
```

## Stopping and Removing the Cluster
To stop and remove all containers:
```sh
docker-compose down
```
To remove persistent storage (⚠️ **Warning: This will delete all data**):
```sh
docker volume rm docker-mariadb-galera_mariadb-data-node1
docker volume rm docker-mariadb-galera_mariadb-data-node2
docker volume rm docker-mariadb-galera_mariadb-data-node3
```

## Notes
- **If a node crashes**, it will automatically rejoin the cluster when restarted.
- **This setup is for local testing**. In production, consider Kubernetes, Swarm, or dedicated DB servers.

## License
MIT License

