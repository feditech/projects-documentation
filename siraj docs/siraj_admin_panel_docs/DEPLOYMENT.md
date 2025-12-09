# Deployment Guide

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Environment Setup](#environment-setup)
- [Local Deployment](#local-deployment)
- [Docker Deployment](#docker-deployment)
- [Kubernetes Deployment](#kubernetes-deployment)
- [Cloud Platform Deployment](#cloud-platform-deployment)
- [CI/CD Pipeline](#cicd-pipeline)
- [Monitoring and Logging](#monitoring-and-logging)
- [Troubleshooting](#troubleshooting)

## Overview

This guide covers deploying the Siraj Admin Panel in various environments, from local development to production cloud platforms.

### Deployment Options

1. **Local Development**: npm start for development
2. **Static Build**: Serve production build with any web server
3. **Docker**: Containerized deployment with Nginx
4. **Kubernetes**: Scalable deployment with Helm charts
5. **Cloud Platforms**: Azure, AWS, GCP

## Prerequisites

### For All Deployments

- Access to backend API endpoint
- Environment variables configured
- SSL certificate (for production)

### For Docker Deployment

- Docker Engine 20.x or higher
- Docker Compose 1.29.x or higher (optional)

### For Kubernetes Deployment

- Kubernetes cluster (1.19+)
- Helm 3.x
- kubectl configured
- Container registry access

### For Cloud Deployment

- Cloud provider account (Azure/AWS/GCP)
- CLI tools installed (az/aws/gcloud)
- Appropriate permissions

## Environment Setup

### Environment Variables

Create environment-specific `.env` files:

#### Development (.env.development)

```bash
REACT_APP_API_URL=http://localhost:8000/api/
REACT_APP_CRAWLER_API_URL=http://localhost:8001/api/
REACT_APP_ENV=development
```

#### Staging (.env.staging)

```bash
REACT_APP_API_URL=https://staging-api.siraj.com/api/
REACT_APP_CRAWLER_API_URL=https://staging-crawler.siraj.com/api/
REACT_APP_ENV=staging
```

#### Production (.env.production)

```bash
REACT_APP_API_URL=https://api.siraj.com/api/
REACT_APP_CRAWLER_API_URL=https://crawler.siraj.com/api/
REACT_APP_ENV=production
```

### Security Considerations

- Never commit `.env` files to version control
- Use secret management services (Azure Key Vault, AWS Secrets Manager)
- Rotate API keys regularly
- Enable HTTPS in production
- Implement CORS policies

## Local Deployment

### Development Server

```bash
# Install dependencies
npm install

# Start development server
npm start
```

The application will be available at `http://localhost:3000`.

### Production Build (Local Testing)

```bash
# Create production build
npm run build

# Install serve globally (if not already installed)
npm install -g serve

# Serve the build
serve -s build -l 3000
```

## Docker Deployment

### Building Docker Image

The included `Dockerfile` uses multi-stage builds for optimized image size.

#### Dockerfile Explanation

```dockerfile
# Stage 1: Build the application
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install --frozen-lockfile
COPY . .
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

#### Build Commands

```bash
# Build image with tag
docker build -t siraj-admin:latest .

# Build with specific version
docker build -t siraj-admin:1.0.0 .

# Build for different platforms (Apple Silicon)
docker buildx build --platform linux/amd64 -t siraj-admin:latest .
```

### Running Docker Container

#### Basic Run

```bash
docker run -d \
  --name siraj-admin \
  -p 80:80 \
  siraj-admin:latest
```

#### Run with Environment Variables

```bash
docker run -d \
  --name siraj-admin \
  -p 80:80 \
  -e REACT_APP_API_URL=https://api.siraj.com/api/ \
  siraj-admin:latest
```

#### Run with Volume Mount (for logs)

```bash
docker run -d \
  --name siraj-admin \
  -p 80:80 \
  -v /var/log/nginx:/var/log/nginx \
  siraj-admin:latest
```

### Docker Compose Deployment

Create `docker-compose.yml`:

```yaml
version: '3.8'

services:
  siraj-admin:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: siraj-admin
    ports:
      - "80:80"
    environment:
      - REACT_APP_API_URL=${REACT_APP_API_URL}
      - REACT_APP_CRAWLER_API_URL=${REACT_APP_CRAWLER_API_URL}
    restart: unless-stopped
    networks:
      - siraj-network
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost/"]
      interval: 30s
      timeout: 10s
      retries: 3

networks:
  siraj-network:
    driver: bridge
```

#### Deploy with Docker Compose

```bash
# Start services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down

# Rebuild and restart
docker-compose up -d --build
```

### Push to Container Registry

#### Docker Hub

```bash
# Tag image
docker tag siraj-admin:latest username/siraj-admin:latest

# Login
docker login

# Push
docker push username/siraj-admin:latest
```

#### Azure Container Registry (ACR)

```bash
# Login to ACR
az acr login --name myregistry

# Tag image
docker tag siraj-admin:latest myregistry.azurecr.io/siraj-admin:latest

# Push
docker push myregistry.azurecr.io/siraj-admin:latest
```

#### AWS ECR

```bash
# Get login password
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin YOUR-ACCOUNT-ID.dkr.ecr.us-east-1.amazonaws.com

# Tag image
docker tag siraj-admin:latest YOUR-ACCOUNT-ID.dkr.ecr.us-east-1.amazonaws.com/siraj-admin:latest

# Push
docker push YOUR-ACCOUNT-ID.dkr.ecr.us-east-1.amazonaws.com/siraj-admin:latest
```

## Kubernetes Deployment

### Helm Chart Structure

```
siraj-fe-admin/
├── Chart.yaml              # Chart metadata
├── values.yaml             # Default configuration values
└── templates/              # Kubernetes resource templates
    ├── deployment.yaml     # Deployment configuration
    ├── service.yaml        # Service configuration
    └── ingress.yaml        # Ingress configuration
```

### Configuration Files

#### Chart.yaml

```yaml
apiVersion: v2
name: siraj-admin
version: 0.1.0
description: Helm chart for siraj-admin (React.js frontend)
type: application
```

#### values.yaml

```yaml
image:
  repository: myregistry.azurecr.io/siraj-admin
  tag: latest
  pullPolicy: Always

service:
  port: 80

ingress:
  enabled: true
  hostname: siraj.local
  path: /
  
replicaCount: 2

resources:
  limits:
    cpu: 500m
    memory: 512Mi
  requests:
    cpu: 250m
    memory: 256Mi

env:
  - name: BACKEND_ENV
    value: "production"
  - name: BACKEND_BASE_URL
    value: "https://api.siraj.com/api"
```

### Deployment Steps

#### 1. Create Namespace (Optional)

```bash
kubectl create namespace siraj
```

#### 2. Install with Helm

```bash
# Install release
helm install siraj-admin . \
  --namespace siraj \
  --values values.yaml

# Install with overrides
helm install siraj-admin . \
  --namespace siraj \
  --set image.tag=v1.0.0 \
  --set replicaCount=3
```

#### 3. Verify Deployment

```bash
# Check pods
kubectl get pods -n siraj

# Check services
kubectl get svc -n siraj

# Check ingress
kubectl get ingress -n siraj

# View logs
kubectl logs -f deployment/siraj-admin -n siraj
```

#### 4. Update Deployment

```bash
# Upgrade release
helm upgrade siraj-admin . \
  --namespace siraj \
  --values values.yaml

# Upgrade with new image
helm upgrade siraj-admin . \
  --namespace siraj \
  --set image.tag=v1.1.0
```

#### 5. Rollback (if needed)

```bash
# View release history
helm history siraj-admin -n siraj

# Rollback to previous version
helm rollback siraj-admin -n siraj

# Rollback to specific revision
helm rollback siraj-admin 2 -n siraj
```

#### 6. Uninstall

```bash
helm uninstall siraj-admin -n siraj
```

### Kubernetes Manifests (Without Helm)

If not using Helm, apply manifests directly:

```bash
# Apply all templates
kubectl apply -f templates/

# Or apply individually
kubectl apply -f templates/deployment.yaml
kubectl apply -f templates/service.yaml
kubectl apply -f templates/ingress.yaml
```

### Scaling

```bash
# Manual scaling
kubectl scale deployment siraj-admin --replicas=5 -n siraj

# Horizontal Pod Autoscaler (HPA)
kubectl autoscale deployment siraj-admin \
  --cpu-percent=80 \
  --min=2 \
  --max=10 \
  -n siraj
```

## Cloud Platform Deployment

### Azure App Service

#### Using Azure CLI

```bash
# Login to Azure
az login

# Create resource group
az group create --name siraj-rg --location eastus

# Create App Service plan
az appservice plan create \
  --name siraj-plan \
  --resource-group siraj-rg \
  --sku B1 \
  --is-linux

# Create web app
az webapp create \
  --name siraj-admin \
  --resource-group siraj-rg \
  --plan siraj-plan \
  --deployment-container-image-name myregistry.azurecr.io/siraj-admin:latest

# Configure environment variables
az webapp config appsettings set \
  --name siraj-admin \
  --resource-group siraj-rg \
  --settings \
  REACT_APP_API_URL=https://api.siraj.com/api/

# Enable continuous deployment
az webapp deployment container config \
  --name siraj-admin \
  --resource-group siraj-rg \
  --enable-cd true
```

#### Configure Custom Domain

```bash
# Add custom domain
az webapp config hostname add \
  --webapp-name siraj-admin \
  --resource-group siraj-rg \
  --hostname admin.siraj.com

# Enable HTTPS
az webapp update \
  --name siraj-admin \
  --resource-group siraj-rg \
  --https-only true
```

### AWS Elastic Beanstalk

#### Using EB CLI

```bash
# Initialize Elastic Beanstalk
eb init -p docker siraj-admin

# Create environment
eb create siraj-admin-prod \
  --instance-type t3.small \
  --min-instances 2 \
  --max-instances 5

# Set environment variables
eb setenv \
  REACT_APP_API_URL=https://api.siraj.com/api/ \
  REACT_APP_ENV=production

# Deploy
eb deploy

# Open application
eb open
```

### Google Cloud Platform (GCP)

#### Using Cloud Run

```bash
# Set project
gcloud config set project siraj-project

# Build and submit image
gcloud builds submit --tag gcr.io/siraj-project/siraj-admin

# Deploy to Cloud Run
gcloud run deploy siraj-admin \
  --image gcr.io/siraj-project/siraj-admin \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated \
  --set-env-vars REACT_APP_API_URL=https://api.siraj.com/api/

# Map custom domain
gcloud run domain-mappings create \
  --service siraj-admin \
  --domain admin.siraj.com \
  --region us-central1
```

## CI/CD Pipeline

### GitHub Actions

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy Siraj Admin

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          
      - name: Install dependencies
        run: npm ci
        
      - name: Run tests
        run: npm test -- --coverage --watchAll=false
        
      - name: Build
        run: npm run build
        env:
          REACT_APP_API_URL: ${{ secrets.API_URL }}

  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Login to Azure Container Registry
        uses: docker/login-action@v2
        with:
          registry: myregistry.azurecr.io
          username: ${{ secrets.ACR_USERNAME }}
          password: ${{ secrets.ACR_PASSWORD }}
      
      - name: Build and push Docker image
        uses: docker/build-push-action@v4
        with:
          context: .
          push: true
          tags: myregistry.azurecr.io/siraj-admin:latest
          
      - name: Deploy to Kubernetes
        uses: azure/k8s-deploy@v4
        with:
          manifests: |
            templates/deployment.yaml
            templates/service.yaml
            templates/ingress.yaml
          images: myregistry.azurecr.io/siraj-admin:latest
```

### Azure DevOps Pipeline

Create `azure-pipelines.yml`:

```yaml
trigger:
  branches:
    include:
      - main

pool:
  vmImage: 'ubuntu-latest'

variables:
  dockerRegistryServiceConnection: 'MyACR'
  imageRepository: 'siraj-admin'
  containerRegistry: 'myregistry.azurecr.io'
  tag: '$(Build.BuildId)'

stages:
- stage: Build
  jobs:
  - job: BuildAndTest
    steps:
    - task: NodeTool@0
      inputs:
        versionSpec: '18.x'
    
    - script: |
        npm ci
        npm run build
      displayName: 'Install and Build'
      env:
        REACT_APP_API_URL: $(API_URL)
    
    - task: Docker@2
      inputs:
        containerRegistry: $(dockerRegistryServiceConnection)
        repository: $(imageRepository)
        command: 'buildAndPush'
        Dockerfile: 'Dockerfile'
        tags: |
          $(tag)
          latest

- stage: Deploy
  dependsOn: Build
  jobs:
  - deployment: DeployToK8s
    environment: 'production'
    strategy:
      runOnce:
        deploy:
          steps:
          - task: HelmDeploy@0
            inputs:
              connectionType: 'Kubernetes Service Connection'
              kubernetesServiceConnection: 'MyK8sCluster'
              command: 'upgrade'
              chartType: 'FilePath'
              chartPath: '.'
              releaseName: 'siraj-admin'
              arguments: '--set image.tag=$(tag)'
```

## Monitoring and Logging

### Application Monitoring

#### Azure Application Insights

```bash
# Install SDK (if using)
npm install @microsoft/applicationinsights-web

# Configure in src/index.js
import { ApplicationInsights } from '@microsoft/applicationinsights-web';

const appInsights = new ApplicationInsights({
  config: {
    instrumentationKey: 'YOUR_INSTRUMENTATION_KEY'
  }
});
appInsights.loadAppInsights();
appInsights.trackPageView();
```

### Container Monitoring

#### Docker Logs

```bash
# View logs
docker logs siraj-admin

# Follow logs
docker logs -f siraj-admin

# View last 100 lines
docker logs --tail 100 siraj-admin
```

#### Kubernetes Logs

```bash
# View pod logs
kubectl logs deployment/siraj-admin -n siraj

# Follow logs
kubectl logs -f deployment/siraj-admin -n siraj

# View logs for specific container
kubectl logs pod-name -c container-name -n siraj

# View logs from all pods
kubectl logs -l app=siraj-admin -n siraj --tail=100
```

### Health Checks

#### Docker Health Check

Already included in `docker-compose.yml`:

```yaml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost/"]
  interval: 30s
  timeout: 10s
  retries: 3
```

#### Kubernetes Probes

Add to `templates/deployment.yaml`:

```yaml
livenessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 30
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 5
  periodSeconds: 5
```

## Troubleshooting

### Common Issues

#### 1. Container Fails to Start

**Symptom**: Container exits immediately

**Solution**:
```bash
# Check logs
docker logs siraj-admin

# Run interactively
docker run -it siraj-admin:latest sh

# Check nginx configuration
docker exec siraj-admin nginx -t
```

#### 2. 502 Bad Gateway in Production

**Symptom**: Nginx returns 502 error

**Solution**:
- Verify backend API is accessible
- Check nginx configuration
- Verify environment variables are set correctly
- Check firewall rules

#### 3. Static Assets Not Loading

**Symptom**: Blank page or missing CSS/JS

**Solution**:
- Check build output in `/usr/share/nginx/html`
- Verify nginx is serving from correct directory
- Check browser console for 404 errors
- Verify `homepage` in package.json

#### 4. Kubernetes Pod CrashLoopBackOff

**Symptom**: Pod continuously restarts

**Solution**:
```bash
# Describe pod
kubectl describe pod <pod-name> -n siraj

# Check events
kubectl get events -n siraj --sort-by='.lastTimestamp'

# Check logs from previous pod
kubectl logs <pod-name> --previous -n siraj
```

#### 5. Image Pull Errors

**Symptom**: ImagePullBackOff error in Kubernetes

**Solution**:
```bash
# Create image pull secret
kubectl create secret docker-registry acr-secret \
  --docker-server=myregistry.azurecr.io \
  --docker-username=<username> \
  --docker-password=<password> \
  -n siraj

# Reference in deployment
imagePullSecrets:
  - name: acr-secret
```

### Performance Optimization

#### Enable Gzip Compression

Update `nginx.conf`:

```nginx
gzip on;
gzip_types text/plain text/css application/json application/javascript text/xml application/xml;
gzip_min_length 1000;
```

#### Enable Caching

```nginx
location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}
```

#### Reduce Image Size

```dockerfile
# Use multi-stage builds (already implemented)
# Remove development dependencies
RUN npm ci --only=production
```

---

## Security Checklist

- [ ] HTTPS enabled in production
- [ ] Environment variables secured
- [ ] CORS properly configured
- [ ] Security headers set in nginx
- [ ] Container runs as non-root user
- [ ] Secrets stored in secure vault
- [ ] Regular security updates applied
- [ ] Access logs monitored
- [ ] Rate limiting implemented

## Support

For deployment issues, contact the DevOps team or refer to:
- [README.md](./README.md) - General documentation
- [PRODUCT.md](./PRODUCT.md) - Product features
- [API.md](./API.md) - API integration

---

**Last Updated**: December 2025
