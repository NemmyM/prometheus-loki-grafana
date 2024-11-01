# Monitoring Stack with Prometheus, Loki, and Grafana

This repository provides a standalone Docker Compose setup for running Prometheus, Loki, and Grafana behind a Nginx reverse proxy.


## Overview

The stack consists of:

- **Prometheus**: Metrics collection and storage
- **Loki**: Log aggregation system
- **Grafana**: Visualization and dashboarding
- **Nginx Gateway**: Reverse proxy with basic authentication
- **MinIO**: Local object storage compatible with AWS S3 APIs

## Prerequisites

Before running the stack, you need to:

Create `.env` and `.htpasswd` files or use the sample ones provided.
The `.env` file is used by Loki for S3-like access to MinIO. Both Loki and MinIO use `.env` for credentials.
The `.htpasswd` file configures Nginx to require basic authentication credentials when accessing Loki and Prometheus.

## Installation

1. **Clone the repository**:

   ```bash
   git clone https://github.com/NemmyM/prometheus-loki-grafana.git
   cd prometheus-loki-grafana
   ```

2. **Set up environment variables**:

   ```bash
   cp env.sample .env
   ```

   - Edit the `.env` file to configure the necessary credentials for Loki and MinIO.

3. **Create the `.htpasswd` file for Nginx basic authentication**:

   ```bash
   htpasswd -c .htpasswd yourusername
   ```

   - Replace `yourusername` with your desired username. You will be prompted to set a password.

4. **Update the `config.alloy` file**:

   - Update the basic authentication section in `config.alloy` with the credentials you just set in the `.htpasswd` file.

5. **Start the stack**:

   ```bash
   docker compose up -d
   ```

## Usage

- **Grafana**: Access at [http://yourhostname:3000](http://yourhostname:3000)

## Caveats

- **Images are set to `latest`**: The Docker Compose configuration uses the `latest` tag for images. To avoid unexpected breaking changes, it's recommended to pin each service to a specific image version.
- **TLS is not enabled**: TLS is not implemented in this setup. For secure communication, you should configure TLS on the Nginx gateway or behind a load balancer that provides TLS termination.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

