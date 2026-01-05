# Prometheus Deployment with Docker

## Overview

This repository demonstrates how to deploy **Prometheus** using **Docker
Compose** and configure it to scrape metrics from multiple sources,
including a sample application. The setup is lightweight, easy to
understand, and ideal for learning or internal demos.

The project satisfies the following goals: - Run Prometheus in Docker -
Configure basic scrape targets - Expose and visualize sample application
metrics

------------------------------------------------------------------------

## Features

-   Dockerized Prometheus setup
-   Basic Prometheus scrape configuration
-   Sample application exposing Prometheus metrics
-   Prometheus Web UI for querying and validation
-   Easy to extend with Grafana, Node Exporter, or OpenTelemetry

------------------------------------------------------------------------

## Prerequisites

Ensure the following are installed on your system: - **Docker** (v20+
recommended) - **Docker Compose** (v2+ recommended) - Web browser (for
Prometheus UI)

Optional: - `curl` or PowerShell for testing endpoints

------------------------------------------------------------------------

## Project Structure

    .
    ├── docker-compose.yml
    ├── prometheus
    │   └── prometheus.yml
    └── sample-app
        ├── Dockerfile
        └── app.py

------------------------------------------------------------------------

## Installation

### 1. Clone the Repository

``` bash
git clone https://github.com/your-username/prometheus-docker-demo.git
cd prometheus-docker-demo
```

### 2. Build and Start Services

``` bash
docker-compose up -d --build
```

------------------------------------------------------------------------

## Configuration

### Prometheus Configuration

Located at `prometheus/prometheus.yml`

``` yaml
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'sample-app'
    static_configs:
      - targets: ['sample-app:8000']
```

------------------------------------------------------------------------

## Usage

### Access Prometheus UI

Open your browser and navigate to:

    http://localhost:9090

### Verify Targets

-   Go to **Status → Targets**
-   Ensure all targets show `UP`

### Generate Sample Metrics

``` bash
curl http://localhost:8000/
```

### Query Metrics

In the Prometheus UI, run:

    sample_app_requests_total

------------------------------------------------------------------------

## Sample Application

The sample app is a simple Python Flask service exposing metrics at:

    /metrics

Metrics include: - HTTP request count - Basic application availability

------------------------------------------------------------------------

## Acceptance Criteria Validation

  Requirement              Status
  ------------------------ --------
  Prometheus running       ✅
  Basic scrape config      ✅
  Sample metrics visible   ✅

------------------------------------------------------------------------

## Future Enhancements

-   Add Grafana dashboards
-   Integrate Node Exporter for host metrics
-   Add OpenTelemetry Collector for centralized telemetry
-   Secure Prometheus with authentication

------------------------------------------------------------------------

## License

MIT License

------------------------------------------------------------------------

## Author

Created for learning and demonstration purposes.
