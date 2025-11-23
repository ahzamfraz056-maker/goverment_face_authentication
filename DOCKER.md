# Docker Deployment Guide

This guide explains how to build and run the Government Face Authentication app using Docker.

## Prerequisites

- Docker installed on your system
- Docker Compose (optional, for easier management)

## Quick Start

### Option 1: Using Docker Compose (Recommended)

```bash
# Build and run
docker-compose up -d

# View logs
docker-compose logs -f

# Stop
docker-compose down
```

The app will be available at: `http://localhost`

### Option 2: Using Docker Commands

```bash
# Build the image
docker build -t government-face-auth .

# Run the container
docker run -d -p 80:80 --name government-face-auth government-face-auth

# View logs
docker logs -f government-face-auth

# Stop the container
docker stop government-face-auth
docker rm government-face-auth
```

## Building for Production

### Build with custom tag

```bash
docker build -t government-face-auth:latest .
```

### Build with specific version

```bash
docker build -t government-face-auth:v1.0.0 .
```

## Running the Container

### Basic run

```bash
docker run -d -p 80:80 government-face-auth
```

### Run with custom port

```bash
docker run -d -p 8080:80 government-face-auth
```

### Run with environment variables

```bash
docker run -d -p 80:80 \
  -e NGINX_HOST=your-domain.com \
  government-face-auth
```

## Docker Compose Options

### Custom port in docker-compose.yml

Edit `docker-compose.yml` and change:
```yaml
ports:
  - "8080:80"  # Change 80 to your desired port
```

### Add environment variables

```yaml
environment:
  - NGINX_HOST=your-domain.com
  - NGINX_PORT=80
```

## Production Deployment

### 1. Build the image

```bash
docker build -t government-face-auth:production .
```

### 2. Tag for registry (if using Docker Hub or private registry)

```bash
docker tag government-face-auth:production your-registry/government-face-auth:latest
```

### 3. Push to registry

```bash
docker push your-registry/government-face-auth:latest
```

### 4. Deploy to server

```bash
docker pull your-registry/government-face-auth:latest
docker run -d -p 80:80 --name government-face-auth --restart unless-stopped your-registry/government-face-auth:latest
```

## Using with HTTPS

For HTTPS, you'll need to:

1. Use a reverse proxy (nginx, traefik, etc.)
2. Or mount SSL certificates and update nginx.conf

### Example with SSL certificates

```bash
docker run -d -p 443:443 \
  -v /path/to/ssl:/etc/nginx/ssl \
  government-face-auth
```

Then update `nginx.conf` to use SSL.

## Troubleshooting

### Container won't start

```bash
# Check logs
docker logs government-face-auth

# Check if port is already in use
netstat -an | grep 80
```

### App not loading

```bash
# Check if container is running
docker ps

# Check nginx configuration
docker exec government-face-auth cat /etc/nginx/conf.d/default.conf
```

### Rebuild after code changes

```bash
# Stop and remove old container
docker-compose down

# Rebuild
docker-compose build --no-cache

# Start again
docker-compose up -d
```

## Image Size Optimization

The current Dockerfile uses multi-stage build which already optimizes the image size. The final image only contains:
- nginx:alpine (small base image)
- Built Angular app files

## Health Checks

The docker-compose.yml includes a health check. To check container health:

```bash
docker ps  # Shows health status
```

## Environment Variables

You can pass environment variables to configure the app:

- `NGINX_HOST`: Server hostname
- `NGINX_PORT`: Server port (default: 80)

## Security Notes

1. The Dockerfile includes security headers in nginx.conf
2. Runs as non-root user (nginx default)
3. Uses Alpine Linux for smaller attack surface
4. Multi-stage build reduces final image size

## Next Steps

1. Configure Back4App credentials in the app before building
2. Deploy to your preferred container platform (AWS ECS, Google Cloud Run, Azure Container Instances, etc.)
3. Set up CI/CD pipeline to automate builds
4. Configure HTTPS with SSL certificates

## Integration with Back4App

Remember: The Docker container serves the frontend only. You still need:
- Back4App backend configured
- Cloud Code deployed
- Parse classes created

The app will connect to Back4App API from the browser, so CORS must be configured in Back4App.

