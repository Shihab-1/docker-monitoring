# Setting Up Node Exporter

Node Exporter is a Prometheus exporter for hardware and OS metrics exposed by *nix kernels. This guide walks you through installing and configuring Node Exporter on a Linux server.

---

## 📥 Download Node Exporter

Download the Node Exporter binary:

```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz

    ⚠️ Make sure to use the latest version and the correct architecture from Node Exporter Releases.

📦 Extract the Archive

tar xvf node_exporter-1.7.0.linux-amd64.tar.gz

🚚 Move the Binary

cd node_exporter-1.7.0.linux-amd64
sudo cp node_exporter /usr/local/bin

(Optional cleanup):

cd ..
rm -rf node_exporter-1.7.0.linux-amd64*

👤 Create Node Exporter User

sudo useradd --no-create-home --shell /bin/false node_exporter
sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter

⚙️ Create systemd Service

Create and open the systemd unit file:

sudo nano /etc/systemd/system/node_exporter.service

Paste the following content:

[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target

Save and exit the editor.
🔄 Enable & Start Node Exporter

sudo systemctl daemon-reload
sudo systemctl enable node_exporter
sudo systemctl start node_exporter

Check service status:

sudo systemctl status node_exporter

🌐 Verify

Node Exporter should now be running and exposing metrics on:

http://<server-ip>:9100/metrics

Make sure to configure your Prometheus server to scrape this endpoint.
