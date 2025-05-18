# 🚀 Enterprise Log Observability Platform

[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)](https://grafana.com/)
[![Loki](https://img.shields.io/badge/Loki-2C3239?style=for-the-badge&logo=loki&logoColor=white)](https://grafana.com/oss/loki/)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com/)

[![Status](https://img.shields.io/badge/Status-Production-green.svg)]()
[![Version](https://img.shields.io/badge/Version-1.0.0-blue.svg)]()

A production-grade, scalable log management and monitoring solution built with Grafana and Loki, orchestrated via Docker Compose. This platform provides centralized log aggregation, real-time monitoring, and advanced analytics capabilities.

## 📋 Architecture Overview

```
log-observability/
├── docker-compose.yml    # Container orchestration and service definitions
├── loki-config.yaml      # Loki configuration for log ingestion and storage
└── README.md             # Technical documentation
```

## 💻 System Requirements

### Hardware Requirements

- CPU: 2+ cores recommended
- RAM: 4GB minimum, 8GB+ recommended
- Storage: 20GB+ available space (SSD recommended)

### Software Requirements

- Ubuntu 20.04 LTS or newer
- Docker Engine 24.0.0 or newer
- Docker Compose v2.20.0 or newer
- Linux kernel 5.4 or newer

## 🛠️ Installation Guide for Ubuntu

### System Preparation

```bash
# Update system packages
sudo apt update && sudo apt upgrade -y

# Install required dependencies
sudo apt install -y ca-certificates curl gnupg lsb-release apt-transport-https
```

### Docker Repository Setup

```bash
# Add Docker's official GPG key
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Add Docker repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Docker Installation

```bash
# Update package index
sudo apt update

# Install Docker components
sudo apt install -y docker-ce docker-ce-cli containerd.io \
  docker-buildx-plugin docker-compose-plugin

# Enable and start Docker service
sudo systemctl enable --now docker
```

### Post-Installation Configuration

```bash
# Add current user to docker group
sudo usermod -aG docker $USER
newgrp docker  # or log out and log back in

# Verify installation
docker --version
docker compose version
```

## 🚀 Deployment

### Environment Setup

```bash
# Clone repository
git clone <repository-url>
cd log-observability

# Create necessary directories
mkdir -p data/grafana data/loki
```

### Service Deployment

```bash
# Start services in detached mode
docker compose up -d

# Verify deployment
docker compose ps
```

### Health Checks

```bash
# Check container status
docker ps

# Inspect container logs
docker compose logs -f

# Verify network connectivity
docker network inspect log-observability_default
```

## 🔌 Service Access and Configuration

### Grafana Dashboard

- Access URL: http://localhost:3000
- Default credentials:
  - Username: admin
  - Password: admin
- Recommended first-time actions:
  - Change default password
  - Configure SMTP for alerts
  - Set up backup strategy

### Loki API

- API Endpoint: http://localhost:3100
- Query Interface: http://localhost:3100/ready
- Metrics: http://localhost:3100/metrics

## ⚙️ Data Source Configuration

### Loki Integration

1. Access Grafana dashboard
2. Navigate to Configuration > Data Sources
3. Click "Add data source"
4. Select "Loki"
5. Configure settings:
   - URL: http://loki:3100
   - Access: Server (default)
   - Basic Auth: Disabled
   - Skip TLS Verify: Enabled (for development)
6. Click "Save & Test"

## 🏢 Enterprise Best Practices

### 🔒 Security

- Implement network segmentation
- Enable TLS encryption
- Configure authentication and authorization
- Regular security audits
- Implement rate limiting
- Use secrets management

### 📊 Monitoring and Maintenance

- Set up health checks
- Configure alerting rules
- Implement log rotation
- Regular backup procedures
- Performance monitoring
- Resource usage tracking

### 🔄 High Availability

- Implement redundancy
- Configure failover
- Load balancing setup
- Data replication
- Disaster recovery plan

### ⚡ Performance Optimization

- Resource allocation
- Query optimization
- Cache configuration
- Storage optimization
- Network tuning

## 🔧 Troubleshooting

### Common Issues

1. Container startup failures

   ```bash
   docker compose logs
   ```

2. Network connectivity

   ```bash
   docker network inspect
   ip a
   ```

3. Permission issues
   ```bash
   ls -la /var/run/docker.sock
   groups $USER
   ```

### Maintenance Commands

```bash
# View logs
docker compose logs -f

# Restart services
docker compose restart

# Clean up resources
docker system prune -f

# Check disk usage
df -h
```

## 📚 Support and Resources

- [Grafana Documentation](https://grafana.com/docs/)
- [Loki Documentation](https://grafana.com/docs/loki/latest/)
- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)

---
