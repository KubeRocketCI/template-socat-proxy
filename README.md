# Socat Proxy Helm Chart Configuration Guide

This Helm chart enables the deployment of Socat as a versatile proxy tool, allowing for flexible network traffic routing and manipulation, including but not limited to establishing connections to cloud-based databases. Below are the steps to configure and deploy the chart to leverage Socat for specific networking requirements:

## 1. Database Configuration

Begin by specifying the configuration values for your target database in the `values.yaml` file. You need to provide the port number specific to your database type and the database connection string.

```yaml
service:
  port: <port>  # Specify the database port. Use 5432 for PostgreSQL or 3306 for MySQL.

endpointURL: ""  # Enter your database connection string here.
```

Replace `<port>` with the appropriate port number and provide the database connection string.

Example for Amazon RDS PostgreSQL:

```yaml
service:
  port: 5432

endpointURL: "example-rds.cluster-abcdefghijkl.us-west-2.rds.amazonaws.com"
```

## 2. Chart Deployment

Deploy the Helm chart into the same Kubernetes namespace where your application is running. This step associates the Socat proxy with your application, allowing for seamless database connectivity.

## 3. Enable Port Forwarding

To access the database through the proxy, enable port forwarding between your local machine and the Kubernetes pod running the Socat proxy. Use the `kubectl port-forward` command with the appropriate database port.

General Syntax:

```bash
kubectl port-forward socat-proxy <db_port>:<db_port>
```

Replace `<db_port>` with the actual database port number.

### Examples

For PostgreSQL:

```bash
kubectl port-forward socat-proxy 5432:5432
```

For MySQL:

```bash
kubectl port-forward socat-proxy 3306:3306
```

By following these instructions, the Socat proxy will be configured and ready to facilitate connections to your cloud database.
