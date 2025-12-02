# docker-metrics

This stack provides Prometheus and Grafana monitoring with a WordPress site and backing MariaDB database.

## Prerequisites
- Docker and Docker Compose

## Configuration
1. Copy `.env` and adjust credentials and ports as needed.
2. Prometheus configuration lives in `prometheus/prometheus.yml` and includes scrape jobs for Prometheus, Grafana, and the node exporter.
3. Grafana automatically provisions a Prometheus data source via `grafana/provisioning/datasources/datasource.yml`.

## Usage
1. Start the stack:
   ```bash
   docker compose up -d
   ```
2. Access the services:
   - Prometheus: http://localhost:$\{PROMETHEUS_PORT:-9090\}
   - Grafana: http://localhost:$\{GRAFANA_PORT:-3000\} (default admin credentials from `.env`)
   - WordPress: http://localhost:$\{WORDPRESS_PORT:-8080\}
3. To reset the Grafana admin password, run:
   ```bash
   docker exec -it grafana grafana-cli admin reset-admin-password "${NEW_PASS}"
   ```

## Services
- **Prometheus**: scrapes metrics according to `prometheus/prometheus.yml`.
- **Grafana**: dashboards backed by the Prometheus data source.
- **Node Exporter**: exposes host metrics on port 9100.
- **WordPress**: runs on Apache with a dedicated MariaDB instance.
- **MariaDB**: stores WordPress data with credentials from `.env`.
