# Modern TIG Stack for InfluxDB 3

The **TIG Stack** is an acronym for three open-source technologies that seamlessly work together to **collect**, **store**, **analyze**, and **visualize** real-time data from servers, APIs, IoT devices—even your smart coffee machine!

- **T**elegraf: Collects system metrics and sends them to InfluxDB.
- **I**nfluxDB 3 (Core or Enterprise): Time-series database to store the metrics.
- **G**rafana: Visualizes data by querying InfluxDB 3 tables.

---

## 🧰 Pre-requisites

- Docker & Docker Compose installed on your machine.
- Git (optional, for version control).
- Code/text editor to update `.env`.

---

## 🚀 Setup Steps

### 1. Clone the Repository

```bash
git clone https://github.com/InfluxCommunity/TIG-Stack-using-InfluxDB-3.git
cd TIG-Stack-using-InfluxDB-3

2. Start InfluxDB 3 Core

docker-compose up -d influxdb3-core

Then, generate the operator token:

docker-compose exec influxdb3-core influxdb3 create token --admin

3. Update .env File

    Open .env in your text editor.

    Paste the generated token string as the value for:

INFLUXDB_TOKEN=your_generated_token_here

4. Start Telegraf & Grafana Services

docker-compose up -d telegraf
docker-compose up -d grafana

Ensure Docker is running in the background.
