# Trustworthiness Framework

A comprehensive digital identity assessment platform for evaluating organizational maturity across key pillars of trustworthiness. The tool provides structured assessments, automated scoring, standards compliance mapping, and detailed PDF reports.

## Docker Deployment

### Pulling the Container from Docker Hub

```bash
docker pull kimbotto/distaf-app:latest
```

### Building the Container Locally

```bash
# Build the image
docker build -t distaf-app .

# Or use docker compose
docker compose build
```

### Running the Container

```
docker run -d \
  --name distaf-app \
  --restart unless-stopped \
  -e NODE_ENV=production \
  -e PORT=3000 \
  -e DB_PATH=/app/data \
  -e SESSION_SECRET=change_in_production \
  -p 3000:3000 \
  -v "$(pwd)/data:/app/data" \
  --network bridge \
  --health-cmd="wget --no-verbose --tries=1 --spider http://localhost:3000/api/health" \
  --health-interval=30s \
  --health-timeout=10s \
  --health-retries=3 \
  --health-start-period=10s \
  kimbotto/distaf-app
```