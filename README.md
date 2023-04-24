# To set up Prometheus, Grafana, Node Exporter (daemonset), and Alertmanager with Docker Compose on an AWS EC2 instance and monitor another server, follow these steps:

1. Install Docker and Docker Compose on your EC2 instance.

2. Create a new directory for your project and create a docker-compose.yml file:
```
mkdir monitoring
cd monitoring
touch docker-compose.yml
```
check in code 

3. Create directories for Prometheus, Alertmanager, and Grafana configurations:

```
mkdir prometheus alertmanager grafana
touch prometheus/prometheus.yml alertmanager/alertmanager.yml
```

####Check prometheus/prometheus.yml####

Replace <EXTERNAL_SERVER_IP> with the IP address of the server you want to monitor. Ensure the Node Exporter is installed and running on the external server.

####  Check alertmanager/alertmanager.yml ####
Replace the email configurations with your own email service provider details, including the SMTP server, username, and password.

4. Configure Grafana to use Prometheus as a data source. Create a new directory for Grafana provisioning:
```
mkdir grafana/provisioning
touch grafana/provisioning/datasources.yaml

```
5. Start your monitoring stack:
```
docker-compose up -d
```
6. This will start Prometheus, Grafana, Node Exporter, and Alertmanager. You can access Grafana on http://<EC2_INSTANCE_IP>:3000 and log in with the username admin and the password secret.

7. Add additional monitoring dashboards to Grafana as needed.
Remember to open the necessary ports on your EC2 instance's security group and ensure that the external server has Node Exporter installed and running.

In this setup, we've used a DaemonSet-like approach for Node Exporter by deploying it in "global" mode. However, this only works within the scope of the Docker Compose deployment. If you need to monitor more servers, you'll need to install and run Node Exporter on each server and add their IP addresses to the prometheus.yml configuration file.