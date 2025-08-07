kk# 📊 Grafana Docker Compose Setup

## 🧭 Introduction to Grafana

Grafana is an open-source platform for monitoring and observability. It allows you to query, visualize, alert on, and analyze your metrics—no matter where they are stored.

This setup uses **Docker Compose** to quickly deploy Grafana in a container, providing a powerful and flexible way to manage and explore your data.

---

## 🐳 Docker Compose Configuration

This project uses a simple `docker-compose.yml` to deploy Grafana:

```yaml
version: "3.8"
services:
  grafana:
    image: grafana/grafana
    container_name: grafana
    restart: unless-stopped
    ports:
     - '3000:3000'
    volumes:
      - grafana-storage:/var/lib/grafana
volumes:
  grafana-storage: {}

🔍 Key Components

    Image: grafana/grafana (official Docker image)

    Ports: 3000:3000 — exposes Grafana’s web interface on your host’s port 3000

    Volume: grafana-storage:/var/lib/grafana — persists Grafana’s data

    Restart Policy: unless-stopped — container restarts automatically unless stopped manually

🚀 Deploying Grafana

    Save the configuration above to a file called docker-compose.yml

    Start Grafana with:

docker-compose up -d

Open your browser and go to:

    http://<your-server-ip>:3000

    Default credentials:

        Username: admin

        Password: admin (you’ll be prompted to change this on first login)

⚙️ Configuring Grafana

Once Grafana is up and running:

    Connect to your data sources (like Prometheus, InfluxDB, etc.)

    Create dashboards to visualize your data

    Set up alerts for proactive monitoring

🛡️ Optional: SSL & Reverse Proxy

For secure access, consider placing Grafana behind an NGINX reverse proxy with SSL (HTTPS) support using a self-signed or Let's Encrypt certificate.

