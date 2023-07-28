# LichessDataStore
Projects that stores a small lichess data on OpenSearch.

## Requirements

- Docker
- Docker Compose

## Setup

### Docker Compose

The provided Docker Compose configuration sets up a deployment of OpenSearch, including two nodes and a dashboard. Here's a breakdown of the configuration:

1. Services:
    - `opensearch-node1`: Represents the first node of the OpenSearch cluster. It uses the `opensearchproject/opensearch:latest` Docker image and is named `opensearch-node1`. The environment variables configure various settings for the node, such as the cluster name, node name, discovery seed hosts, initial cluster manager nodes, and JVM heap sizes. The container has volume `opensearch-data1` mounted for storing data. Ports 9200 and 9600 are exposed to allow REST API and performance analyzer access. The service is connected to the `opensearch-net` network.
    - `opensearch-node2`: Represents the second node of the OpenSearch cluster. It has similar configuration to `opensearch-node1`, including the same Docker image, environment variables, volume, and network. Ports 9200 and 9600 are not explicitly mapped since they are already mapped in `opensearch-node1`.
    - `opensearch-dashboards`: Represents the OpenSearch Dashboards component. It uses the `opensearchproject/opensearch-dashboards:latest` Docker image and is named `opensearch-dashboards`. Port 5601 is mapped to allow access to the dashboards. The `OPENSEARCH_HOSTS` environment variable specifies the OpenSearch nodes that Dashboards will query. The service is connected to the `opensearch-net` network.

2. Volumes:
    - `opensearch-data1` and `opensearch-data2`: These volumes are created to store the data for the OpenSearch nodes. They are mounted to their respective containers.

3. Networks:
    - `opensearch-net`: This network is created for connecting the OpenSearch containers. All the services are part of this network.

The configuration allows you to run a distributed OpenSearch cluster with two nodes (`opensearch-node1` and `opensearch-node2`) and access OpenSearch Dashboards at `http://localhost:5601`. Make sure you have Docker installed and run the `docker-compose up` command in the directory where the `docker-compose.yml` file is located to start the deployment.

run the following command to start the deployment:

### Windows

```bash
Update the `vm.max_map_count` setting on your host machine:
```bash
wsl -d docker-desktop
sysctl -w vm.max_map_count=262144
```

```bash
docker-compose up
```

