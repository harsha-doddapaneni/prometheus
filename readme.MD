# Prometheus

![alt text](prometheus.svg)

Reference: https://prometheus.io/download/

* move to /opt directory
```
cd /opt/
```
```
wget https://github.com/prometheus/prometheus/releases/download/v3.0.1/prometheus-3.0.1.linux-amd64.tar.gz
```

* Extract tar file
```
tar -xf prometheus-3.0.1.linux-amd64.tar.gz
```

* Rename if required

```
mv prometheus-3.0.1.linux-amd64 prometheus
```

* Create systemctl service
```
vim /etc/systemd/system/prometheus.service
```

* Enter below info
```
[Unit]
Description=Prometheus Server

[Service]
ExecStart=/opt/prometheus/prometheus --config.file=/opt/prometheus/prometheus.yml

[Install]
WantedBy=multi-user.target
```

```
systemctl start prometheus
```
```
systemctl enable prometheus
```

* node-1

```
cd /opt/
```

```
https://github.com/prometheus/node_exporter/releases/download/v1.9.1/node_exporter-1.9.1.linux-amd64.tar.gz
```

```
tar -xf node_exporter-1.9.1.linux-amd64.tar.gz
```

```
mv node_exporter-1.9.1.linux-amd64 node_exporter
```

```
vim /etc/systemd/system/node_exporter.service
```
```
[Unit]
Description=Node Exporter

[Service]
ExecStart=/opt/node_exporter/node_exporter

[Install]
WantedBy=multi-user.target
```

```
systemctl restart node_exporter
```

```
systemctl status node_exporter
```

```
systemctl enable node_exporter
```

* grafana

```
curl -o gpg.key https://rpm.grafana.com/gpg.key
```
```
sudo rpm --import gpg.key
```

```
vim /etc/yum.repos.d/grafana.repo
```
```
[grafana]
name=grafana
baseurl=https://rpm.grafana.com
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://rpm.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
```

```
sudo dnf install grafana
```
```
systemctl daemon-reload
```

```
systemctl start grafana-server
```
