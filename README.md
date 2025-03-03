# Prometheus Monitoring

![](image.png)
- P.S. Automation vs Monitoring (Me answering, there is nothing to monitor in case there is no automation, which this project proves wrong)

## Overview 
This project sets up a **Docker-based monitoring stack** using:
- **Prometheus** (for collecting metrics)
- **Node Exporter** (for system metrics)
- **Grafana** (for visualization)

The containerization approach was used as the project does not manage multiple servers, just one - which is my localhost. So Docker-based environment provides a minimal setup maintaining simplicity and fast deployment.

## Taken Steps:
### **Initial Setup**
- Created a **`docker-compose.yaml`** file to manage the services.

### **Configuring Prometheus**
- Downloading the latest Prometheus container image 
- Configuring scrape metrics for Prometheus
- Introducing 1-minute policy: Alerting in case Node Exporter is down for more than 1 minute
- Setting default ports(9090:9090)
- Added a health check to verify Prometheus availability.

### **Configuring Node_Exporter**
- Downloading the latest Node_Exporter container image 
- Setting default ports(9100:9100)
- Configured health check to ensure Node Exporter is running.

### **Configuring Grafana**
- Downloading the latest Grafana container image 
- Setting default ports(3000)
- Configuring Prometheous as a datasource
- Vizualising the basic metrcis (UP/DOWN Status for services/ alert)
- Importing dashboards for Prometheus monitoring
- Used volumes for persistent Grafana data
- Future improvement: Secure Grafana using environment variables

### **Ensuring Services Restart on Failure and Reboot**
- Used **`restart: always`** in docker-compose.yml in order to ensure all services restart automatically on failure or reboot

### Which Prometheus exporter can be used to monitor SSL certificate expiration dates?
There are multiple exporters available for this task, including:

- node-cert-exporter: Extracts certificate expiration details.
- Repository: https://github.com/amimof/node-cert-exporter

- blackbox-exporter: Probes endpoints for SSL/TLS certificate expiration monitoring.
- Repository: https://github.com/prometheus/blackbox_exporter

## How to use
Before running the monitoring stack, ensure that Docker and Docker Compose are installed.
For Ubuntu/Linux

# Install Docker
sudo apt update
sudo apt install -y docker.io

# Install Docker Compose
sudo apt install -y docker-compose

# Enable Docker service to start on boot
sudo systemctl enable docker
sudo systemctl start docker

### **Start the Monitoring Stack**
Run the following command to start all services: **`docker-compose up -d`**
### **Access the Services**
- Prometheus UI: http://localhost:9090
    - Targets: http://localhost:9090/targets (See active exporters)
    - Alerts: http://localhost:9090/alerts (View triggered alerts)
- Node Exporter Metrics: http://localhost:9100/metrics
- Grafana Dashboard: http://localhost:3000 (Default login: admin/admin)

