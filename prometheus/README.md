# 📈 Prometheus Docker Compose Setup

## 🔍 Introduction to Prometheus

Prometheus is an open-source monitoring and alerting toolkit widely used for its:

- Efficient time-series data storage
- Powerful query language (PromQL)
- Integration with numerous exporters like Node Exporter, Blackbox, and more

This repository provides a Docker Compose setup to easily deploy Prometheus with a custom configuration file.

---

## 🐳 Docker Compose Configuration

Below is the `docker-compose.yml` used to run Prometheus in a container:

```yaml
version: '3.8'
services:
  prometheus:
    image: prom/prometheus
    container_name: prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
    ports:
      - 9090:9090
    restart: unless-stopped
    volumes:
      - ./prometheus:/etc/prometheus
      - prom_data:/prometheus
volumes:
  prom_data:

⚙️ Prometheus Configuration File

Create a prometheus.yml inside a prometheus/ directory:

global:
  scrape_interval: 15s
  scrape_timeout: 10s
  evaluation_interval: 15s

alerting:
  alertmanagers:
    - static_configs:
      - targets: []
      scheme: http
      timeout: 10s
      api_version: v2

scrape_configs:
  - job_name: prometheus
    honor_timestamps: true
    scrape_interval: 15s
    scrape_timeout: 10s
    metrics_path: /metrics
    scheme: http
    static_configs:
      - targets:
        - localhost:9090

  - job_name: Sufian  # Change to any identifier you like
    static_configs:
      - targets: ['192.168.1.1:9100']  # Replace with your server's IP address

🧱 Key Components

    Image: prom/prometheus – official Prometheus Docker image

    Command: Loads the custom configuration file located at /etc/prometheus/prometheus.yml

    Ports: 9090:9090 maps host to container port for web access

    Volumes:

        ./prometheus:/etc/prometheus – mounts local config directory

        prom_data:/prometheus – persists time-series data

    Restart Policy: unless-stopped keeps Prometheus running unless stopped manually

🚀 Deployment Steps

    Create the following directory structure:

prometheus-setup/
├── docker-compose.yml
└── prometheus/
    └── prometheus.yml

From the root folder, start Prometheus:

docker-compose up -d

Open your browser and go to:

    http://<your-server-ip>:9090

🛠️ Modifying Configuration

    To add new targets (e.g., other exporters or services), update the prometheus.yml file inside the prometheus/ directory.

    Restart Prometheus to apply changes:

    docker-compose restart prometheus

🌐 Example Use Cases

    Monitor Linux system metrics using Node Exporter

    Track Docker container metrics using cAdvisor

    Visualize metrics in Grafana by adding Prometheus as a data source.
