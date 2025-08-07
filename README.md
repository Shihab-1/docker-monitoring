cat > README.md << 'EOF'
# Docker Monitoring Stack

Contains configuration for:
- Grafana
- Prometheus
- Node Exporter
- InfluxDB
- Nginx with SSL

## Setup

1. Clone this repository
2. Copy environment template:
   ```bash
   cp .env.template .env
