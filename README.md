
# Kubernetes Setup for NGINX, Fluent Bit, and Elasticsearch

This repository provides Kubernetes configuration files to easily set up a deployment involving NGINX, Fluent Bit, and Elasticsearch. The setup is designed to collect NGINX logs, process them with Fluent Bit, and store the logs in an Elasticsearch database for easy querying and visualization.

## Prerequisites

- Kubernetes cluster
- kubectl configured to access the cluster
- curl command-line tool
- Basic knowledge of Kubernetes, Fluent Bit, NGINX, and Elasticsearch

## Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/your-username/your-repo.git
   cd your-repo
   ```

2. **Deploy the configuration files:**

   Apply the Kubernetes manifests for NGINX, Fluent Bit, and Elasticsearch.

   ```bash
   kubectl apply -f k8s/nginx-deployment.yaml
   kubectl apply -f k8s/fluent-bit-deployment.yaml
   kubectl apply -f k8s/elasticsearch-deployment.yaml
   ```

3. **Verify the deployment:**

   Check the status of the pods to ensure they are running correctly:

   ```bash
   kubectl get pods
   ```

## Generating Logs

To generate logs in the NGINX server, use the following `curl` command to send a request to the NGINX service:

```bash
curl http://<nginx-service-ip>/your-endpoint
```

This will trigger a log entry in the NGINX logs, which Fluent Bit will collect and forward to Elasticsearch.

## Access Elasticsearch

You can access Elasticsearch for querying logs:

1. Port-forward Elasticsearch to your local machine:

   ```bash
   kubectl port-forward service/elasticsearch 9200:9200
   ```

2. Use curl or any Elasticsearch client to interact with the database. Example query to retrieve logs:

   ```bash
   curl -X GET "localhost:9200/your-index/_search?pretty"
   ```

## Components

- **NGINX:** Acts as the web server and generates logs for HTTP requests.
- **Fluent Bit:** Collects the logs from NGINX and forwards them to Elasticsearch.
- **Elasticsearch:** Stores the logs in a searchable database for analysis.

## Cleanup

To clean up the deployed resources, run:

```bash
kubectl delete -f k8s/nginx-deployment.yaml
kubectl delete -f k8s/fluent-bit-deployment.yaml
kubectl delete -f k8s/elasticsearch-deployment.yaml
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
